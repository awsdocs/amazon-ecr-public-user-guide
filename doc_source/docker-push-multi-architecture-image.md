# Pushing a multi\-architecture image<a name="docker-push-multi-architecture-image"></a>

Amazon ECR Public supports creating and pushing Docker manifest lists which are used for multi\-architecture images\. A *manifest list* is a list of images that is created by specifying one or more image names\. Typically the manifest list is created from images that serve the same function but for different operating systems or architectures, but this is not required\. For more information, see [docker manifest](https://docs.docker.com/engine/reference/commandline/manifest/)\.

**Important**  
Your Docker CLI must have experimental features enabled to use this feature\. For more information, see [Experimental features](https://docs.docker.com/engine/reference/commandline/cli/#experimental-features)\.

A manifest list can be pulled or referenced in an Amazon ECS task definition or Amazon EKS pod spec like other Amazon ECR Public images\.

The following steps can be used to create and push a Docker manifest list to an Amazon ECR public repository\. You must already have the images pushed to your public repository to reference in the Docker manifest\. For information on pushing an image, see [Pushing a public image](docker-push-ecr-image.md)\.

**To push a multi\-architecture Docker image to an Amazon ECR public repository**

1. Authenticate your Docker client to the Amazon ECR public registry to which you intend to push your image\. Authentication tokens are valid for 12 hours\. For more information, see [Registry authentication](public-registries.md#public-registry-auth)\.

1. List the images in your public repository, confirming the image tags\.

   ```
   aws ecr-public describe-images \
        --repository-name my-web-app
        --region us-east-1
   ```

1. Create the Docker manifest list\. The `manifest create` command verifies that the referenced images are already in your public repository and creates the manifest locally\.

   ```
   docker manifest create public.ecr.aws/registry_alias/my-web-app public.ecr.aws/registry_alias/my-web-app:image_one_tag public.ecr.aws/registry_alias/my-web-app:image_two
   ```

1. \(Optional\) Inspect the Docker manifest list\. This enables you to confirm the size and digest for each image manifest referenced in the manifest list\.

   ```
   docker manifest inspect public.ecr.aws/registry_alias/my-web-app
   ```

1. Push the Docker manifest list to your Amazon ECR public repository\.

   ```
   docker manifest push public.ecr.aws/registry_alias/my-web-app
   ```