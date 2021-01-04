# Pushing a public image<a name="docker-push-ecr-image"></a>

You can push your Docker images to an Amazon ECR public repository with the docker push command\.

**Important**  
Amazon ECR requires that users have permission to make calls to the `ecr-public:GetAuthorizationToken` and `sts:GetServiceBearerToken` API through an IAM policy before they can authenticate to a registry and push any images to an Amazon ECR repository\.

Amazon ECR Public also supports creating and pushing Docker manifest lists which are used for multi\-architecture images\. Each image referenced in a manifest list must already be pushed to your repository\. For more information, see [Pushing a multi\-architecture image](docker-push-multi-architecture-image.md)\.

**To push a Docker image to an Amazon ECR public repository**

1. Authenticate your Docker client to the Amazon ECR public registry to which you intend to push your image\. Authentication tokens are valid for 12 hours\. For more information, see [Registry authentication](public-registries.md#public-registry-auth)\.

1. If your public repository does not exist in the registry you intend to push to yet, create it\. For more information, see [Creating a public repository](public-repository-create.md)\.

1. Identify the image to push\. Run the docker images command to list the images on your system\.

   ```
   docker images
   ```

   You can identify an image with the *repository:tag* value or the image ID in the resulting command output\.

1. <a name="image-tag-step"></a>Tag your image with the Amazon ECR public registry, public repository, and optional image tag name combination to use\. The public registry format is `public.ecr.aws/registry_alias`\. The public repository name should match the repository that you created for your image\. If you omit the image tag, we assume that the tag is `latest`\.

   The following example tags an image with the ID *e9ae3c220b23* as `public.ecr.aws/registry_alias/my-web-app`

   ```
   docker tag e9ae3c220b23 public.ecr.aws/registry_alias/my-web-app
   ```

1. <a name="image-push-step"></a>Push the image using the docker push command:

   ```
   docker push public.ecr.aws/registry_alias/my-web-app
   ```

1. \(Optional\) Apply any additional tags to your image and push those tags to Amazon ECR Public by repeating [Step 4](#image-tag-step) and [Step 5](#image-push-step)\. You can apply up to 1000 tags per image in Amazon ECR Public\.