# Amazon ECR Public managed IAM policies<a name="public-ecr-managed-policies"></a>

Amazon ECR Public provides several managed policies that you can attach to IAM users or EC2 instances that allow differing levels of control over Amazon ECR resources and API operations\. You can apply these policies directly, or you can use them as starting points for creating your own policies\. For more information about each API operation mentioned in these policies, see [Actions](https://docs.aws.amazon.com/AmazonECRPublic/latest/APIReference/API_Operations.html) in the *Amazon ECR Public API Reference*\.

**Topics**
+ [`AmazonElasticContainerRegistryPublicFullAccess`](#AmazonElasticContainerRegistryPublicFullAccess)
+ [`AmazonElasticContainerRegistryPublicPowerUser`](#AmazonElasticContainerRegistryPublicPowerUser)
+ [`AmazonElasticContainerRegistryPublicReadOnly`](#AmazonElasticContainerRegistryPublicReadOnly)

## `AmazonElasticContainerRegistryPublicFullAccess`<a name="AmazonElasticContainerRegistryPublicFullAccess"></a>

The `AmazonElasticContainerRegistryPublicFullAccess` managed policy is a starting point when looking to provide an IAM user or role with full administrator access to manage their use of Amazon ECR Public\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecr-public:*",
                "sts:GetServiceBearerToken"
            ],
            "Resource": "*"
        }
    ]
}
```

## `AmazonElasticContainerRegistryPublicPowerUser`<a name="AmazonElasticContainerRegistryPublicPowerUser"></a>

The `AmazonElasticContainerRegistryPublicPowerUser` managed policy allows power user access to Amazon ECR Public, which allows write access to public repositories, but does not allow users to delete public repositories or change the policy documents applied to them\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecr-public:GetAuthorizationToken",
                "sts:GetServiceBearerToken",
                "ecr-public:BatchCheckLayerAvailability",
                "ecr-public:GetRepositoryPolicy",
                "ecr-public:DescribeRepositories",
                "ecr-public:DescribeRegistries",
                "ecr-public:DescribeImages",
                "ecr-public:DescribeImageTags",
                "ecr-public:GetRepositoryCatalogData",
                "ecr-public:GetRegistryCatalogData",
                "ecr-public:InitiateLayerUpload",
                "ecr-public:UploadLayerPart",
                "ecr-public:CompleteLayerUpload",
                "ecr-public:PutImage"
            ],
            "Resource": "*"
        }
    ]
}
```

## `AmazonElasticContainerRegistryPublicReadOnly`<a name="AmazonElasticContainerRegistryPublicReadOnly"></a>

The `AmazonElasticContainerRegistryPublicReadOnly` managed policy allows read\-only access to Amazon ECR Public\. This includes the ability to describe public registries, list and describe public repositories, and describe images within a public repository\.

```
{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "ecr-public:GetAuthorizationToken",
            "sts:GetServiceBearerToken",
            "ecr-public:BatchCheckLayerAvailability",
            "ecr-public:GetRepositoryPolicy",
            "ecr-public:DescribeRepositories",
            "ecr-public:DescribeRegistries",
            "ecr-public:DescribeImages",
            "ecr-public:DescribeImageTags",
            "ecr-public:GetRepositoryCatalogData",
            "ecr-public:GetRegistryCatalogData"
        ],
        "Resource": "*"
    }]
}
```