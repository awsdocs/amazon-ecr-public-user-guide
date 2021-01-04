# Creating a public repository<a name="public-repository-create"></a>

Before you can push your Docker or Open Container Initiative \(OCI\) images to Amazon ECR, you must create a repository to store them in\. Public repositories are visible on the Amazon ECR Public Gallery and are open to publicly pull images from\. If you want to create a private repository instead, see [Repositories](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Repositories.html) in the *Amazon Elastic Container Registry User Guide*\.

**To create a public repository \(AWS Management Console\)**

1. Open the Amazon ECR console at [https://console\.aws\.amazon\.com/ecr/](https://console.aws.amazon.com/ecr/)\.

1. From the navigation bar, choose the Region to create your public repository in\.

1. In the navigation pane, choose **Repositories**\.

1. On the **Repositories** page, choose **Create repository**\.

1. For **Visibility settings**, choose **Public**\.

1. For **Repository name**, enter a unique name for your public repository\. The repository name may be specified on its own \(such as `nginx-web-app`\) or it can be prepended with a namespace to group the repository into a category \(such as `project-a/nginx-web-app`\)\.

1. For **Repository logo**, choose **Upload file** and select a local image file to use as the repository logo\. Amazon ECR uploads your logo as a base64\-encoded payload to a publicly available Amazon S3 bucket\.
**Note**  
The repository logo is only publicly visible in the Amazon ECR Public Gallery for verified accounts\.

1. For **Short description** enter a description of the repository\. The description field is displayed on the Amazon ECR Public Gallery in the search results and on the repository detail page\.

1. For **Content types** select the operating system and system architecture tags to associate with the repository\. These tags are publicly displayed in the Amazon ECR Public Gallery as badges on the repository and are used as search filters\.

1. For **About**, enter a detailed description for the repository\. This field is publicly visible on the Amazon ECR Public Gallery on the repository detail page\.

1. For **Usage**, enter details about how to use the images in the repository\. This field is publicly visible on the Amazon ECR Public Gallery on the repository detail page\.

1. Choose **Create repository**\.