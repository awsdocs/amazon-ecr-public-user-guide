# Amazon ECR Public service quotas<a name="public-service-quotas"></a>

The following table provides the default service quotas for Amazon ECR Public\.


****  

| Service quota | Description | Default quota value | 
| --- | --- | --- | 
|  Registered repositories  |  The maximum number of repositories that you can create per Region\.  |  10,000  | 
|  Image per repository  |  The maximum number of images per repository\.  |  10,000  | 
|  Image pulls \*  |  The maximum number of image pulls per second\.  |  1 for unauthenticated pulls 10 for authenticated pulls  | 

\* There are separate rate limits for unauthenticated \(guest\) and authenticated image pulls\. An authenticated image pull is one that includes an authentication token from Amazon ECR and are per account\. An unauthenticated \(guest\) pull does not include an authentication token and are per source IP address\. We recommend authenticating with your AWS account when pulling images for use on AWS\. For more information, see [Registry authentication](public-registries.md#public-registry-auth)\.

The following table provides the default rate quotas for each of the Amazon ECR API actions involved with the authentication and image pushes\.


****  
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonECR/latest/public/public-service-quotas.html)

The following table provides other quotas for Amazon ECR and Docker images that cannot be changed\.

**Note**  
The layer part information mentioned in the following table is only applicable if you are calling the Amazon ECR Public API actions directly to initiate multipart uploads for image push operations\. This is a rare action\. We recommend that you use the Docker CLI to pull, tag, and push images\.


| Service quota | Description | Quota value | 
| --- | --- | --- | 
|  Layer parts  |  The maximum number of layer parts\. This is only applicable if you are using Amazon ECR API actions directly to initiate multipart uploads for image push operations\.  |  1,000  | 
|  Maximum layer size  |  The maximum size \(MiB\) of a layer\. \*\*  |  10,000  | 
|  Minimum layer part size  |  The minimum size \(MiB\) of a layer part\. This is only applicable if you are using Amazon ECR API actions directly to initiate multipart uploads for image push operations\.  |  5  | 
|  Maximum layer part size  |  The maximum size \(MiB\) of a layer part\. This is only applicable if you are using Amazon ECR API actions directly to initiate multipart uploads for image push operations\.  |  10  | 
|  Destination registry IDs in a replication rule  |  The maximum number of registry IDs that can be specified as a replication destination in a replication rule\. This is used when configuring cross\-account replication\.  |  25  | 
|  Tags per image  |  The maximum number of tags per image\.  |  1000  | 

\*\* The maximum layer size listed here is calculated by multiplying the maximum layer part size \(10 MiB\) by the maximum number of layer parts \(1,000\)\.