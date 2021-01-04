# Deleting a public image<a name="public-image-delete"></a>

If you are done using an image, you can delete it from your public repository\. You can delete an image using the AWS Management Console, or the AWS CLI\.

**Note**  
If you are done with a public repository, you can delete the entire repository and all of the images within it\. For more information, see [Deleting a public repository](public-repository-delete.md)\.

**To delete a public image with the AWS Management Console**

1. Open the Amazon ECR console at [https://console\.aws\.amazon\.com/ecr/repositories](https://console.aws.amazon.com/ecr/repositories)\.

1. From the navigation bar, choose the Region that contains the image to delete\.

1. In the navigation pane, choose **Repositories**\.

1. On the **Repositories** page, select the **Public** tab and then select the repository containing the image to delete\.

1. On the **Repositories: *repository\_name*** page, select the box to the left of the image to delete and choose **Delete**\.

1. In the **Delete image\(s\)** dialog box, verify that the selected images should be deleted and choose **Delete**\.

**To delete a public image with the AWS CLI**

1. List the image tags in your repository\.

   ```
   aws ecr-public describe-image-tags \
         --repository-name my-repo \
         --region us-east-1
   ```

1. \(Optional\) Delete any unwanted tags for the image by specifying the tag of the image you want to delete\.
**Note**  
When you delete the last tag for an image, the image is deleted\.

   ```
   aws ecr-public batch-delete-image \
         --repository-name my-repo \
         --image-ids imageTag=latest \
         --region us-east-1
   ```

1. Delete the image by specifying the digest of the image to delete\.
**Note**  
When you delete an image by referencing its digest, the image and all of its tags are deleted\.

   ```
   aws ecr-public batch-delete-image \
         --repository-name my-repo \
         --image-ids imageDigest=sha256:4f70ef7a4d29e8c0c302b13e25962d8f7a0bd304c7c2c1a9d6fa3e9de6bf552d
         --region us-east-1
   ```