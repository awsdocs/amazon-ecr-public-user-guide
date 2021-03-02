# Quick start: Publishing to Amazon ECR Public using the AWS CLI<a name="getting-started-cli"></a>

This quick start guide walks you through the steps needed to create a Docker image, publish the image to a public repository, pull the image down from the Amazon ECR Public Gallery, and then clean up the resources using the Docker CLI and the AWS CLI\.

For more information on the other tools available for managing your AWS resources, including the different AWS SDKs, IDE toolkits, and the Windows PowerShell command line tools, see [http://aws\.amazon\.com/tools/](http://aws.amazon.com/tools/)\.

## Prerequisites<a name="cli-prerequisites"></a>

Before you begin, be sure that you've completed the steps in [Setting up with Amazon ECR](get-set-up-for-amazon-ecr.md)\.

To build, tag, and push container images to your Amazon ECR public repositories you must have the AWS CLI and a container CLI client, for example Docker\. Docker is a common tool for building container images\. For more information about how to install Docker, see [Docker installation guide](https://docs.docker.com/engine/installation/#installation)\.

To use the AWS CLI with Amazon ECR Public, install the latest AWS CLI version\. For information, see [Installing the AWS CLI version 2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) in the *AWS Command Line Interface User Guide*\.

## Step 1: Create a Docker image<a name="cli-create-image"></a>

In this step, you create a Docker image of a simple web application, and test it on your local system or Amazon EC2 instance\.

**To create a Docker image of a simple web application**

1. Create a file called `Dockerfile`\. A Dockerfile is a manifest that describes the base image to use for your Docker image and what you want installed and running on it\. For more information about Dockerfiles, go to the [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)\.

   ```
   touch Dockerfile
   ```

1. Edit the `Dockerfile` you just created and add the following content\.

   ```
   FROM public.ecr.aws/amazonlinux/amazonlinux:latest
   
   # Install dependencies
   RUN yum update -y && \
    yum install -y httpd
   
   # Install apache and write hello world message
   RUN echo 'Hello World!' > /var/www/html/index.html
   
   # Configure apache
   RUN echo 'mkdir -p /var/run/httpd' >> /root/run_apache.sh && \
    echo 'mkdir -p /var/lock/httpd' >> /root/run_apache.sh && \
    echo '/usr/sbin/httpd -D FOREGROUND' >> /root/run_apache.sh && \
    chmod 755 /root/run_apache.sh
   
   EXPOSE 80
   
   CMD /root/run_apache.sh
   ```

   This Dockerfile uses the public Amazon Linux 2 image hosted on Amazon ECR Public\. The `RUN` instructions update the package caches, installs some software packages for the web server, and then write the "Hello World\!" content to the web server's document root\. The `EXPOSE` instruction exposes port 80 on the container, and the `CMD` instruction starts the web server\.

1. <a name="sample-docker-build-step"></a>Build the Docker image from your Dockerfile\.
**Note**  
Some versions of Docker may require the full path to your Dockerfile in the following command, instead of the relative path shown below\.

   ```
   docker build -t hello-world .
   ```

1. List your container image\.

   ```
   docker images --filter reference=hello-world
   ```

   Output:

   ```
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   hello-world         latest              e9ffedc8c286        4 minutes ago       194MB
   ```

1. Run the newly built image\. The `-p 80:80` option maps the exposed port 80 on the container to port 80 on the host system\. For more information about docker run, go to the [Docker run reference](https://docs.docker.com/engine/reference/run/)\.

   ```
   docker run -t -i -p 80:80 hello-world
   ```
**Note**  
Output from the Apache web server is displayed in the terminal window\. You can ignore the "`Could not reliably determine the server's fully qualified domain name`" message\.

1. Open a browser and point to the server that is running Docker and hosting your container\.
   + If you are using an EC2 instance, this is the **Public DNS** value for the server, which is the same address you use to connect to the instance with SSH\. Make sure that the security group for your instance allows inbound traffic on port 80\.
   + If you are running Docker locally, point your browser to [http://localhost/](http://localhost/)\.
   + If you are using docker\-machine on a Windows or Mac computer, find the IP address of the VirtualBox VM that is hosting Docker with the docker\-machine ip command, substituting *machine\-name* with the name of the docker machine you are using\.

     ```
     docker-machine ip machine-name
     ```

   You should see a web page with your "Hello World\!" statement\.

1. Stop the Docker container by typing **Ctrl \+ c**\.

## Step 2: Authenticate to a public registry<a name="cli-authenticate-registry"></a>

After you have installed and configured the AWS CLI, authenticate the Docker CLI to your public registry\. That way, the docker command can push to and pull images from an Amazon ECR public repository\. The AWS CLI provides a get\-login\-password command to simplify the authentication process\.

To authenticate Docker to an Amazon ECR public registry with get\-login\-password, run the aws ecr\-public get\-login\-password \-\-region us\-east\-1 command\. The Amazon ECR Public registry requires authentication in the `us-east-1` Region, so you need to specify `--region us-east-1` each time you authenticate\. The authentication token received gives you access to each public registry your IAM principal has access to\. When passing the authentication token to the docker login command, use the value `AWS` for the username and specify `public.ecr.aws`, which is the common public registry URI\.

**Important**  
If you receive an error, install or upgrade to the latest version of the AWS CLI\. For more information, see [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) in the *AWS Command Line Interface User Guide*\.

```
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
```

## Step 3: Create a public repository<a name="cli-create-repository"></a>

Now that you have an image to push to Amazon ECR Public, you can create a public repository\. In this example, you create a public repository called `ecr-tutorial` to which you later push the `hello-world:latest` image\. All public repositories that contain an image are publicly visible in the Amazon ECR Public Gallery so we will specify some catalog data for the repository\.

Create a file named `repositorycatalogdata.json` with the following contents\. For this tutorial we are going to include a repository logo, which is named `myrepoimage.png` and is in the same directory as the `repositorycatalogdata.json` file we are creating\.

**Note**  
When creating a repository logo, the supported image dimensions for both height and width should be a minimum of 60 pixels and a maximum of 2048 pixels\. The maximum logo file size is 500 KB\.

```
{
    "description": "This is a test repo for an Amazon ECR tutorial.",
    "architectures": [
        "x86"
    ],
    "operatingSystems": [
        "Linux"
    ],
    "logoImageBlob": "$(cat myrepoimage.png |base64 -w 0)",
    "aboutText": "This repository is used as a tutorial only.",
    "usageText": "This repository is not for public use."
}
```

Use the catalog data file we just created to run the following `create-repository` command\. Your repository URI is included in the response, which you will need in the next step for pushing an image to the repository\.

```
aws ecr-public create-repository \
     --repository-name ecr-tutorial \
     --catalog-data file://repositorycatalogdata.json \
     --region us-east-1
```

## Step 4: Push an image to Amazon ECR Public<a name="cli-push-image"></a>

Now you can push your image to the Amazon ECR public repository you created in the previous section\. You use the Docker CLI to push images, but there are a few prerequisites that must be satisfied for this to work properly:
+ The Amazon ECR Public authorization token has been configured with docker login\.
+ The Amazon ECR public repository exists and the user has access to push to the repository\.

After those prerequisites are met, you can push your image to your newly created repository in the default registry for your account\.

**To tag and push an image to Amazon ECR Public**

1. List the images you have stored locally to identify the image to tag and push\.

   ```
   docker images
   ```

   Output:

   ```
   REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
   hello-world         latest              e9ffedc8c286        4 minutes ago       241MB
   ```

1. Tag the image to push to your repository with your public repository URI which was in the response to the `create-repository` call you made in the previous step\.

   ```
   docker tag hello-world:latest public.ecr.aws/registry_alias/ecr-tutorial
   ```

1. Push the image\.

   ```
   docker push public.ecr.aws/registry_alias/ecr-tutorial
   ```

   Output:

   ```
   The push refers to a repository [public.ecr.aws/registry_alias/ecr-tutorial] (len: 1)
   e9ae3c220b23: Pushed
   a6785352b25c: Pushed
   0998bf8fb9e9: Pushed
   0a85502c06c9: Pushed
   latest: digest: sha256:215d7e4121b30157d8839e81c4e0912606fca105775bb0636b95EXAMPLE size: 1569
   ```

## Step 5: Pull an image from the Amazon ECR Public Gallery<a name="cli-pull-image"></a>

After your image has been pushed to your Amazon ECR public repository, you can pull it from other locations\. It is considered best practice to authenticate prior to pulling images from the public gallery\. If you need to reauthenticate, see [Step 2: Authenticate to a public registry](#cli-authenticate-registry)\.

**Note**  
Unauthenticated pulls are allowed, but have a lower rate limit than authenticated pulls\. For more information, see [Amazon ECR Public service quotas](public-service-quotas.md)\.

View your repository on the Amazon ECR Public Gallery\.

```
https://gallery.ecr.aws/registry_alias/ecr-tutorial
```

```
docker pull public.ecr.aws/registry_alias/ecr-tutorial/hello-world:latest
```

## Step 6: Delete a public image<a name="cli-delete-image"></a>

If you decide that you no longer need or want an image in one of your repositories, you can delete it with the batch\-delete\-image command\. To delete an image, you must specify the repository that it is in and either a `imageTag` or `imageDigest` value for the image\. The example below deletes an image in the `hello-world` repository with the image tag `latest`\.

```
aws ecr-public batch-delete-image \
      --repository-name ecr-tutorial \
      --image-ids imageTag=latest \
      --region us-east-1
```

## Step 7: Delete a public repository<a name="cli-delete-repository"></a>

If you decide that you no longer need or want an entire repository of images, you can delete the repository\. By default, you cannot delete a repository that contains images; however, the `--force` flag allows this\. To delete a repository that contains images \(and all the images within it\), run the following command\.

```
aws ecr-public delete-repository \
      --repository-name ecr-tutorial \
      --force \
      --region us-east-1
```