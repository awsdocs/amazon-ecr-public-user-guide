# Viewing public repository information<a name="public-repository-info"></a>

After you have created a public repository, you can view details about it in the AWS Management Console\. For each image in the repository, you can view the image tags, when it was last pushed, the size, the URI for pulling, and SHA digest\. The catalog data for the Amazon ECR Public Gallery can be reviewed\. You can also see the repository permission policies associated with the repository\.

**Note**  
Beginning with Docker version 1\.9, the Docker client compresses image layers before pushing them to a V2 Docker registry\. The output of the docker images command shows the uncompressed image size, so it may return a larger image size than the image sizes shown in the AWS Management Console\.

**To view public repository information**

1. Open the Amazon ECR console at [https://console\.aws\.amazon\.com/ecr/repositories](https://console.aws.amazon.com/ecr/repositories)\.

1. From the navigation bar, choose the Region that contains the repository to view\.

1. In the navigation pane, choose **Repositories**\.

1. On the **Repositories** page, select the **Public** tab and then choose the repository to view the details of\.

1. On the **Repositories > *repository\_name*** page, choose **View public listing** to navigate to the repository detail page in the Amazon ECR Public Gallery in a new tab or use the navigation bar to view more details about the repository\.
   + Choose **Images** to view information about the images in the repository\. If there are untagged images that you would like to delete, you can select the box to the left of the repositories to delete and choose **Delete**\. For more information, see [Deleting a public image](public-image-delete.md)\.
   + Choose **Gallery detail** to view the public catalog data for the repository\. 
   + Choose **Permissions** to view the repository policies that are applied to the repository\. For more information, see [Public repository policies](public-repository-policies.md)\.