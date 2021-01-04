# Pulling a public image<a name="docker-pull-ecr-image"></a>

If you would like to run a Docker image that is available in Amazon ECR Public, you can pull it to your local environment with the docker pull command\. You can do this from any public repository\. Every public repository hosted on Amazon ECR Public is available on the Amazon ECR Public Gallery\. Visit the Amazon ECR Public Gallery at [https://gallery\.ecr\.aws](https://gallery.ecr.aws)\. For more information, see [Using the Amazon ECR Public Gallery](public-gallery.md)\.

**Important**  
Amazon ECR requires that users have permission to make calls to the `ecr-public:GetAuthorizationToken` and `sts:GetServiceBearerToken` API through an IAM policy before they can authenticate to a registry and push any images to an Amazon ECR repository\.

**To pull a public image from the Amazon ECR Public Gallery**

1. Identify the image to pull\. You can view the available public repositories on the Amazon ECR Public Gallery at [https://gallery\.ecr\.aws](https://gallery.ecr.aws)\.

1. Authenticate your Docker client to the Amazon ECR public registry\. Authentication tokens are valid for 12 hours\. For more information, see [Registry authentication](public-registries.md#public-registry-auth)\.

1. Pull the image using the docker pull command\. The image name format should be `registry_alias/repository[:tag]` to pull by tag, or `registry_alias/repository[@digest]` to pull by digest\.

   ```
   docker pull public.ecr.aws/registry_alias/amazonlinux:latest
   ```