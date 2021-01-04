# Amazon ECR public repositories<a name="public-repositories"></a>

Amazon Elastic Container Registry provides API operations to create, monitor, and delete public image repositories and set permissions that control who can push images to them\. You can perform the same actions in the **Repositories** section of the Amazon ECR console\. Amazon ECR integrates with the Docker CLI to push images from your development environments to your public repositories\.

A public repository is open to publicly pull images from and is visible on the Amazon ECR Public Gallery\. When creating a public repository you specify catalog data which helps users find and use your images\. For more information about the Amazon ECR Public Gallery, see [Using the Amazon ECR Public Gallery](public-gallery.md)\.

**Topics**
+ [Public repository concepts](#public-repository-concepts)
+ [Creating a public repository](public-repository-create.md)
+ [Editing a public repository](public-repository-edit.md)
+ [Repository catalog data](public-repository-catalog-data.md)
+ [Viewing public repository information](public-repository-info.md)
+ [Deleting a public repository](public-repository-delete.md)
+ [Public repository policies](public-repository-policies.md)

## Public repository concepts<a name="public-repository-concepts"></a>
+ The public repositories you create that contain images appear publicly on the Amazon ECR Public Gallery\. Visit the Amazon ECR Public Gallery at [https://gallery\.ecr\.aws](https://gallery.ecr.aws)\. For more information, see [Using the Amazon ECR Public Gallery](public-gallery.md)\.
+ By default, your account has read and write access to the repositories in your public registry\. However, IAM users require permissions to make calls to the Amazon ECR APIs and to push images to your repositories\.
+ Public repositories can be controlled with both IAM user access policies and repository policies\. For more information, see [Public repository policies](public-repository-policies.md)\.