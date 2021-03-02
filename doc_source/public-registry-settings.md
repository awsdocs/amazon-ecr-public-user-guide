# Updating registry settings<a name="public-registry-settings"></a>

Your public registry provides settings to configure a custom alias and display name\.

By default, your public registry is assigned a **default alias** after your first public repository is created\. You can request a **custom alias** for your registry, and if approved, both the default alias and custom alias can be used to access your public repositories\. The registry **display name** appears on each repository in the Amazon ECR Public Gallery if your account has been verified\. For non\-verified accounts, the display name can be configured but it will not be visible\.

When requesting a custom alias, the following words or phrases should be avoided:
+ An alias that includes `aws`, `amazon`, or the name of an AWS service
+ An alias using a company name for which you do not have permission to use
+ Generic names, such as `test`, `public`, and `marketplace`
+ Offensive, inappropriate, or non\-inclusive words and phrases

Use the following steps to edit your public registry settings\.

**To edit public registry settings \(AWS Management Console\)**

1. Open the Amazon ECR console at [https://console\.aws\.amazon\.com/ecr/](https://console.aws.amazon.com/ecr/)\.

1. From the navigation bar, choose the Region to edit your public registry settings in\.

1. In the navigation pane, choose **Registries**\.

1. On the **Registries** page, select your **Public** registry and then choose **Edit**\.

1. For **Custom alias**, enter a custom alias to request\.

1. For **Display name**, enter a display name for your registry\.

1. Choose **Save changes**\.