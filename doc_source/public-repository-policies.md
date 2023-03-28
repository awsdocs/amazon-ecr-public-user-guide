# Public repository policies<a name="public-repository-policies"></a>

Amazon ECR uses resource\-based permissions to control access to public repositories\. Resource\-based permissions let you specify which IAM users or roles have access to a public repository and what actions they can perform on it\. By default, only the repository owner has access to a repository\. With public repositories, anyone can pull images from the repository but only the repository owner has access to push to the repository\. You can apply a policy document to allow additional permissions to your repository\.

## Repository policies vs IAM policies<a name="repository-policy-vs-iam-policy"></a>

Amazon ECR public repository policies are a subset of IAM policies that are scoped for, and specifically used for, controlling access to individual Amazon ECR repositories\. IAM policies are generally used to apply permissions for the entire Amazon ECR service but can also be used to control access to specific resources as well\.

Both Amazon ECR repository policies and IAM policies are used when determining which actions a specific IAM user or role may perform on a repository\. If a user or role is allowed to perform an action through a repository policy but is denied permission through an IAM policy \(or vice versa\) then the action will be denied\. A user or role only needs to be allowed permission for an action through either a repository policy or an IAM policy but not both for the action to be allowed\.

**Important**  
Amazon ECR requires that users have permission to make calls to the `ecr-public:GetAuthorizationToken` and `sts:GetServiceBearerToken` API through an IAM policy before they can authenticate to a registry and push any images to an Amazon ECR repository\.

You can use either of these policy types to control access to your public repositories, as shown in the following examples\.

This example shows an Amazon ECR public repository policy, which allows for a specific IAM user to describe the repository and the images within the repository\.

```
{
  "Version": "2008-10-17",
  "Statement": [{
    "Sid": "ECR Public Repository Policy",
    "Effect": "Allow",
    "Principal": {
      "AWS": "arn:aws:iam::account-id:user/username"
    },
    "Action": [
       "ecr-public:DescribeImages",
       "ecr-public:DescribeRepositories"
    ]
  }]
}
```

This example shows an IAM policy that achieves the same goal as above, by scoping the policy to a public repository \(specified by the full Amazon Resource Name \(ARN\) of the public repository\) using the resource parameter\. For more information about ARN format, see [Resources](security_iam_service-with-iam.md#security_iam_service-with-iam-id-based-policies-resources)\.

```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "ECR Public Repository Policy",
    "Effect": "Allow",
    "Action": [
      "ecr-public:DescribeImages",
      "ecr-public:DescribeRepositories"
    ],
    "Resource": [
      "arn:aws:ecr-public::account-id:repository/repository-name"
    ]
    }]
}
```

**Topics**
+ [Repository policies vs IAM policies](#repository-policy-vs-iam-policy)
+ [Setting a repository policy statement](set-public-repository-policy.md)
+ [Deleting a public repository policy statement](delete-public-repository-policy.md)
+ [Public repository policy examples](public-repository-policy-examples.md)
