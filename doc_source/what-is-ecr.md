# What Is Amazon Elastic Container Registry Public?<a name="what-is-ecr"></a>

Amazon Elastic Container Registry Public is a managed AWS container image registry service that is secure, scalable, and reliable\. Amazon ECR supports public image repositories with resource\-based permissions using AWS IAM so that specific users can access your public repositories to push images\. Developers can use their preferred CLI to push and manage Docker images, Open Container Initiative \(OCI\) images, and OCI compatible artifacts\. Your images are publicly available to pull, either anonymously or using an Amazon ECR Public authentication token\.

**Note**  
Amazon ECR supports private container image repositories as well\. For more information, see [What is Amazon ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html) in the *Amazon Elastic Container Registry User Guide*\.

The AWS container services team maintains a public roadmap on GitHub\. It contains information about what the teams are working on and allows all AWS customers the ability to give direct feedback\. For more information, see [AWS Containers Roadmap](https://github.com/aws/containers-roadmap)\.

## Components of Amazon ECR Public<a name="ecr-components"></a>

Amazon ECR Public contains the following components:

Amazon ECR Public Gallery  
The Amazon ECR Public Gallery is the public portal that lists all public repositories hosted on Amazon ECR Public\. Visit the Amazon ECR Public Gallery at [https://gallery\.ecr\.aws](https://gallery.ecr.aws)\. For more information, see [Using the Amazon ECR Public Gallery](public-gallery.md)\.

Registry  
A public registry is provided to each AWS account; you can create public image repositories in your public registry and store images in them\. For more information, see [Amazon ECR public registries](public-registries.md)\.

Authorization token  
Your client must authenticate to a public registry as an AWS user before it can push images to a public repository\. For image pulls, Amazon ECR Public accepts both anonymous pulls and pulls using an authentication token\. For more information, see [Registry authentication](public-registries.md#public-registry-auth)\.

Repository  
An Amazon ECR image repository contains your Docker images, Open Container Initiative \(OCI\) images, and OCI compatible artifacts\. For more information, see [Amazon ECR public repositories](public-repositories.md)\.

Repository policy  
You can control access to your repositories and the images within them with repository policies\. For more information, see [Public repository policies](public-repository-policies.md)\.

Image  
You can push and pull container images to your repositories\. You can use these images locally on your development system, or you can use them in Amazon ECS task definitions and Amazon EKS pod specifications\.