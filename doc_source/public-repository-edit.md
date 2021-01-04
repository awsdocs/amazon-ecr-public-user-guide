# Editing a public repository<a name="public-repository-edit"></a>

An existing public repository can be edited to change the catalog data details that are visible in the Amazon ECR Public Gallery\.

**To edit a repository**

1. Open the Amazon ECR console at [https://console\.aws\.amazon\.com/ecr/repositories](https://console.aws.amazon.com/ecr/repositories)\.

1. From the navigation bar, choose the Region that contains the repository to edit\.

1. In the navigation pane, choose **Repositories**\.

1. On the **Repositories** page, select the **Public** tab and then select the repository to edit and choose **Edit**\.

1. For **Repository logo**, if your repository doesn't have a logo then choose **Upload file** and select a local image file to use as the repository logo\. If your repository has a logo currently, choose **Replace file** to choose a new logo file\. Choose **Reset** to reset your logo selection\.
**Note**  
The repository logo is only publicly visible in the Amazon ECR Public Gallery for verified accounts\.

1. For **Short description** edit the description of the repository\. The description field is displayed on the Amazon ECR Public Gallery in the search results and on the repository detail page\.

1. For **Content types** select the operating system and system architecture tags to associate with the repository\. These tags are publicly displayed in the Amazon ECR Public Gallery as badges on the repository and are used as search filters\.

1. For **About**, enter a detailed description for the repository\. This field is publicly visible on the Amazon ECR Public Gallery on the repository detail page\. This text should be in GitHub Flavored Markdown format\. For examples, see [Repository catalog data](public-repository-catalog-data.md)\.

1. For **Usage**, enter details about how to use the images in the repository\. This field is publicly visible on the Amazon ECR Public Gallery on the repository detail page\. This text should be in GitHub Flavored Markdown format\. For examples, see [Repository catalog data](public-repository-catalog-data.md)\.

1. Choose **Save** to update the repository settings\.