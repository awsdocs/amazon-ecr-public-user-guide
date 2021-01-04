# Amazon ECR public registries<a name="public-registries"></a>

Amazon ECR public registries host your container images in a highly available and scalable architecture, allowing you to deploy containers reliably for your applications\. You can use your public registry to manage public image repositories consisting of Docker and Open Container Initiative \(OCI\) images\. Each AWS account is provided with a default public and private Amazon ECR registry\. For information about private registries, see [Amazon ECR registries](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html) in the *Amazon Elastic Container Registry User Guide\.* 

**Topics**
+ [Public registry concepts](#public-registry-concepts)
+ [Registry authentication](#public-registry-auth)
+ [Updating registry settings](public-registry-settings.md)

## Public registry concepts<a name="public-registry-concepts"></a>

The following concepts apply to your public registry\.
+ A default alias is assigned to your public registry after creating your first public repository\. A custom alias can be requested in the public registry settings in the Amazon ECR console\.
+ Each repository you create in your public registry is available publicly in the Amazon ECR Public Gallery\. The Amazon ECR Public Gallery is available at `https://gallery.ecr.aws`\. The URL to access a repository in your public registry on the Amazon ECR Public Gallery is `https://gallery.ecr.aws/registry_alias/repository_name`\.
**Note**  
Any active alias for your public registry can be used\. This includes both the default alias and custom alias for your public registry\.
+ The URI to use when pulling images from a repository in your public registry is `public.ecr.aws/registry_alias/repository_name:image_tag`\.
**Note**  
Any active alias for your public registry can be used\. This includes both the default alias and custom alias for your public registry\.
+ By default, your account has read and write access to the repositories in your private registry\. However, IAM users require permissions to make calls to the Amazon ECR APIs and to push images to your repositories\. Anyone will be able to pull images from your public repository from the Amazon ECR Public Gallery\.
+ You must authenticate your Docker client to your public registry so that you can use the docker push command to push images to the repositories in your public registry\. For more information, see [Registry authentication](#public-registry-auth)\.
+ Repositories can be controlled with both IAM user access policies and repository policies\. For more information about repository policies, see [Public repository policies](public-repository-policies.md)\.

## Registry authentication<a name="public-registry-auth"></a>

You can use the AWS Management Console, the AWS CLI, or the AWS SDKs to create and manage public repositories\. You can also use those methods to perform some actions on images, such as listing or deleting them\. These clients use standard AWS authentication methods\. Although technically you can use the Amazon ECR Public API to push and pull images, you are much more likely to use the Docker CLI or a language\-specific Docker library\.

The Docker CLI does not support native IAM authentication methods\. Additional steps must be taken so that Amazon ECR can authenticate and authorize Docker push and pull requests\.

The following registry authentication methods are available\.

### Using an authorization token<a name="public-registry-auth-token"></a>

The permission scope of an authorization token matches that of the IAM principal used to retrieve the authentication token\. An authentication token is used to access any Amazon ECR public registry that your IAM principal has access to and is valid for 12 hours\. The authentication token is also used to pull any images from a public repository on the Amazon ECR Public Gallery\. To obtain an authorization token, you must use the [GetAuthorizationToken](https://docs.aws.amazon.com/AmazonECRPublic/latest/APIReference/API_GetAuthorizationToken.html) API operation to retrieve a base64\-encoded authorization token containing the username `AWS` and an encoded password\. The AWS CLI `get-login-password` command simplifies this by retrieving and decoding the authorization token which you can then pipe into a docker login command to authenticate\.

#### To authenticate Docker to an Amazon ECR registry with get\-login\-password<a name="get-login-password"></a>

To authenticate Docker to an Amazon ECR registry with get\-login\-password, run the aws ecr\-public get\-login\-password command\. When passing the authentication token to the docker login command, use the value `AWS` for the username and specify the Amazon ECR registry URI you want to authenticate to\. When authenticating to a public registry, always authenticate to the `us-east-1` Region when using the AWS CLI\.

**Important**  
If you receive an error, install or upgrade to the latest version of the AWS CLI\. For more information, see [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) in the *AWS Command Line Interface User Guide*\.

[get\-login\-password](https://docs.aws.amazon.com/cli/latest/reference/ecr/get-login-password.html) \(AWS CLI\)

```
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
```

### Using HTTP API authentication<a name="registry_auth_http"></a>

Amazon ECR Public supports the [Docker Registry HTTP API](https://docs.docker.com/registry/spec/api/)\. However, you must provide an authorization token with every HTTP request\. You can add an HTTP authorization header using the `-H` option for curl and pass the authorization token provided by the get\-authorization\-token AWS CLI command\.

**To authenticate with the Amazon ECR HTTP API**

1. Retrieve an authorization token with the AWS CLI and set it to an environment variable\.

   ```
   TOKEN=$(aws ecr-public get-authorization-token --region us-east-1 --output=text --query 'authorizationData.authorizationToken')
   ```

1. To authenticate to the API, pass the `$TOKEN` variable to the `-H` option of curl\. For example, the following command lists the manifest details for an image in an Amazon ECR public repository\. For more information, see the [Docker Registry HTTP API](https://docs.docker.com/registry/spec/api/) reference documentation\.

   ```
   curl -i -H "Authorization: Bearer $TOKEN" https://public.ecr.aws/v2/registry_alias/repository_name/manifests/image_tag
   ```

   Output:

   ```
   HTTP/1.1 200 OK
   Date: Mon, 30 Nov 2020 16:20:09 GMT
   Content-Type: application/vnd.docker.distribution.manifest.v2+json
   Content-Length: 1569
   Connection: keep-alive
   Docker-Distribution-Api-Version: registry/2.0
   
   {
      "schemaVersion": 2,
      "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
      "config": {
         "mediaType": "application/vnd.docker.container.image.v1+json",
         "size": 3854,
         "digest": "sha256:2599adbc30c28b1ee5f25a5ebabcc40a37eb81bd89e6f837989ce0fEXAMPLE"
      },
      "layers": [
         {
            "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
            "size": 26708056,
            "digest": "sha256:f22ccc0b8772d8e1bcb40f137b373686bc27427a70c0e41dd22b3801EXAMPLE"
         },
         {
            "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
            "size": 850,
            "digest": "sha256:3cf8fb62ba5ffb221a2edb2208741346eb4d2d99a174138e4afbb69ceEXAMPLE"
         },
         {
            "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
            "size": 162,
            "digest": "sha256:e80c964ece6a3edf0db1cfc72ae0e6f0699fb776bbfcc92b708fbb945EXAMPLE"
         },
         {
            "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
            "size": 56322511,
            "digest": "sha256:9f379ca76d09bc8d1647896e7dc2d9de21b772fd49cb9f21114de76EXAMPLE"
         },
         {
            "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
            "size": 190,
            "digest": "sha256:d8a5f6eb23fabfe50ebb6facb8c46aa2b2ca0b3a455fe631c312034EXAMPLE"
         },
         {
            "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
            "size": 207,
            "digest": "sha256:69c1ea2550a94189f95691ed2538c44a2635f988b7cf0d5425f5b4aEXAMPLE"
         }
      ]
   }
   ```