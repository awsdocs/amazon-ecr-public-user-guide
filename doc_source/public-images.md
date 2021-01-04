# Public images<a name="public-images"></a>

Amazon ECR Public stores Docker images, Open Container Initiative \(OCI\) images, and OCI compatible artifacts in repositories\. You can use the Docker CLI or your preferred client to push and pull images to and from your repositories\.

**Important**  
Amazon ECR requires that users have permission to make calls to the `ecr-public:GetAuthorizationToken` and `sts:GetServiceBearerToken` API through an IAM policy before they can authenticate to a registry and push any images to an Amazon ECR repository\.

**Topics**
+ [Pushing a public image](docker-push-ecr-image.md)
+ [Pushing a multi\-architecture image](docker-push-multi-architecture-image.md)
+ [Pushing a Helm chart](push-oci-artifact.md)
+ [Pulling a public image](docker-pull-ecr-image.md)
+ [Deleting a public image](public-image-delete.md)
+ [Container image manifest formats](image-manifest-formats.md)