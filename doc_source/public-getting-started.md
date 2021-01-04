# Getting started with Amazon ECR Public<a name="public-getting-started"></a>

Get started with Amazon ECR public repositories by creating your first public repository and setting your public registry settings in the Amazon ECR console\. The Amazon ECR console guides you through the process to get started\.

## Prerequisites<a name="public-getting-started-prerequisites"></a>

Before you begin, be sure that you've completed the steps in [Setting up with Amazon ECR](get-set-up-for-amazon-ecr.md)\.

To build, tag, and push container images to your Amazon ECR public repositories you must have the AWS CLI and a CLI client, for example the Docker CLI, to do this\. Docker is a common tool for building container images\. Docker is available on many different operating systems, including most modern Linux distributions, like Ubuntu, and even Mac OSX and Windows\. You don't need a local development system to use Docker\. If you are using Amazon EC2 already, you can launch an Amazon EC2 instance and install Docker to get started\. For more information about how to install Docker on your particular operating system, go to the [Docker installation guide](https://docs.docker.com/engine/installation/#installation)\.

To use the AWS CLI with Amazon ECR Public, install the latest AWS CLI version\. For information about installing the AWS CLI or upgrading to the latest version, see [Installing the AWS CLI version 2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) in the *AWS Command Line Interface User Guide*\.

## Create a public repository<a name="public-getting-started-create-repository"></a>

**To create a public image repository \(AWS Management Console\)**

A repository is where you store your Docker or Open Container Initiative \(OCI\) images in Amazon ECR that you want to make publicly available for others to pull\.

1. Open the Amazon ECR console at [https://console\.aws\.amazon\.com/ecr/get\-started](https://console.aws.amazon.com/ecr/)\.

1. Choose **Get Started**\.

1. For **Visibility settings**, choose **Public**\.

1. For **Repository name**, enter a unique name for your public repository\.

1. \(Optional\) For **Repository logo**, choose **Upload file** and select a local image file to use as the repository logo\.
**Note**  
The repository logo is only publicly visible in the Amazon ECR Public Gallery for verified accounts\. A verified account is an account that is AWS Marketplace certified\.

1. For **Short description** enter a description of the repository\. The description field is displayed on the Amazon ECR Public Gallery in the search results and on the repository detail page\.

1. For **Content types** select the operating system and system architecture tags to associate with the repository\. These tags are publicly displayed in the Amazon ECR Public Gallery as badges on the repository and are used as search filters\.

1. For **About**, enter a detailed description for the repository\. This text should be in Github Flavored Markdown format\. For format examples, see [Repository catalog data](public-repository-catalog-data.md)\. This field is publicly visible on the Amazon ECR Public Gallery on the repository detail page\.

1. For **Usage**, enter details about how to use the images in the repository\. This text should be in Github Flavored Markdown format\. For format examples, see [Repository catalog data](public-repository-catalog-data.md)\. This field is publicly visible on the Amazon ECR Public Gallery on the repository detail page\.

1. Choose **Create repository**\.

## Push a Docker image<a name="public-getting-started-build-push-image"></a>

**Build, tag, and push a Docker image**

You can build, tag, and push a container image using the Docker CLI\. You can use a container image that you have built from a Dockerfile or one that you pulled from another registry, such as a private Amazon ECR repository or Docker Hub and then push the tagged image to your public repository\. For more detailed steps on using the Docker CLI, see \.

1. Select the public repository you created and choose **View push commands** to view the steps to push an image to your new repository\.

1. Run the login command that authenticates your Docker client to your registry by pasting the command from the console into a terminal window\. This command provides an authorization token that is valid for 12 hours\.

1. \(Optional\) If you have a Dockerfile for the image to push, build the image and tag it for your new repository\. Pasting the docker build command from the console into a terminal window\. Make sure that you are in the same directory as your Dockerfile\.

1. Tag the image with the URI of your public registry and your new repository by pasting the docker tag command from the console into a terminal window\. The console command assumes that your image was built from a Dockerfile in the previous step\. If you did not build your image from a Dockerfile, replace the first instance of `repository:latest` with the image ID or image name of your local image to push\.

1. Push the newly tagged image to your repository by pasting the docker push command into a terminal window\.

1. Choose **Close**\.

## Edit the registry settings<a name="public-getting-started-edit-registry"></a>

**\(Optional\) To edit your public registry settings**

Each AWS account is provided with a default public Amazon ECR registry\. The public registry is assigned a default alias after you have created your first public repository or requested a custom alias\. Once Amazon ECR approves your custom alias request, it will appear when describing your registry as well as on your public repositories on the Amazon ECR Public Gallery\.

The registry alias is part of the repository URI that is used to pull the images in the public repository\. The following steps walk you through requesting a custom alias and setting a display name for your registry\.

1. Open the Amazon ECR console at [https://console\.aws\.amazon\.com/ecr/](https://console.aws.amazon.com/ecr/)\.

1. From the navigation bar, choose the Region to edit your public registry settings in\.

1. In the navigation pane, choose **Registries**\.

1. On the **Registries** page, select your **Public** registry and then choose **Edit**\.

1. For **Custom alias**, enter a custom alias to request\. 

1. For **Display name**, enter a display name for your registry\.

1. Choose **Save changes**\.