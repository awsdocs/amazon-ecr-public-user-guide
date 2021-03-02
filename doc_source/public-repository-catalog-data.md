# Repository catalog data<a name="public-repository-catalog-data"></a>

When you create a public repository, you specify catalog data which helps users find, understand, and use the images in the repository\. The catalog data you configure for a public repository includes a short description, the operating system and system architecture compatibilities, an optional logo, an **About** section which provides a more detailed description, and an **Usage** section which provides details on how to use the images\.

When specifying a logo, it is specified as a blob which is a base64\-encoded string\. The supported image dimensions for both height and width should be a minimum of 60 pixels and a maximum of 2048 pixels\. The maximum file size is 500 KB\. To generate a blob from an existing PNG file, you could use the following commmand:

```
cat myrepoimage.png | base64
```

The text for the **About** and **Usage** should be in GitHub Flavored Markdown format\. When using the API, SDK, or AWS CLI to format the text, you should use `/n` to indicate a line break\.

The following table provides examples for specifying certain element types in your `About` and `Usage` sections of your repository catalog data\.

## Examples<a name="public-repository-catalog-data-examples"></a>

The following are examples of how to format the **About** and **Usage** repository catalog data so it appears properly on the Amazon ECR Public Gallery\.\.

**Topics**
+ [Example: Headings](#example-headings)
+ [Example: Text formatting](#example-textformatting)
+ [Example: Code formatting](#example-codeformatting)
+ [Example: Links](#example-links)
+ [Example: Lists](#example-lists)
+ [Example: Full **About** description](#example-abouttext)
+ [Example: Full **Usage** description](#example-usagetext)

### Example: Headings<a name="example-headings"></a>

Headings are designated by the number sign \(`#`\)\. A single number sign and a space indicate a top\-level heading, two number signs create a second\-level heading, and three number signs create a third\-level heading, as in the following examples\.

**AWS Management Console**  
The following example is how you would format headings using the console\.

```
# Heading level one

Body text

## Heading level two

Body text

### Heading level three

Body text
```

**AWS CLI**  
The following example is how you would format headings using the AWS CLI\.

```
# Heading level one\n\nBody text\n\n## Heading level two\n\nBody text\n\n### Heading level three\n\nBody text\n\n#### Heading level four\n\nBody text
```

### Example: Text formatting<a name="example-textformatting"></a>

Text formatting is used to format text as italic, bold, or strikethrough\. The syntax for text formating is the same for both the console and the AWS CLI\.

```
*This text appears in italics*
```

```
**This text appears in bold**
```

```
~~This text appears in strikethrough~~
```

### Example: Code formatting<a name="example-codeformatting"></a>

Code formatting is used to format monospace text or multi\-line codeblocks\. The syntax for code formating is the same for both the console and the AWS CLI\.

```
`code text`
```

```
```
multi-line
codeblock
```
```

### Example: Links<a name="example-links"></a>

A clickable web link is formatted by using `link_text` surrounded by square brackets, followed by the full URL in parentheses\. The syntax for text formating is the same for both the console and the AWS CLI\.

```
[What is Amazon Elastic Container Registry?](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)
```

### Example: Lists<a name="example-lists"></a>

To format lines as part of a bulleted list, type them on separate lines with a single asterisk and then a space, at the beginning of the line\. To format lines as part of a numbered list, type them on separate lines with a number, period, and space at the beginning of the line\.

**AWS Management Console**  
The following example is how you would format lists using the console\.

```
* Bullet 1
* Bullet 2
* Bullet 3
```

```
1. Step one
2. Step two
3. Step three
```

**AWS CLI**  
The following example is how you would format lists using the AWS CLI\.

```
* Bullet 1\n* Bullet 2\n* Bullet 3
```

```
1. Step one\n2. Step two\n3. Step three
```

### Example: Full **About** description<a name="example-abouttext"></a>

The following screenshot from the Amazon ECR Public Gallery displays how an **About** section could be constructed\. We show how to format this text using both the AWS Management Console and the AWS CLI\.

![\[Example - Repository About\]](http://docs.aws.amazon.com/AmazonECR/latest/public/images/catalog-data-about.png)

**AWS Management Console**  
The following is how you would format the screenshot above using the console\.

```
## Quick reference

Maintained by: [the Amazon Linux Team](https://github.com/aws/amazon-linux-docker-images)

Where to get help: [the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://dockr.ly/slack), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)

## Supported tags and respective `dockerfile` links

* [`2.0.20200722.0`, `2`, `latest`](https://github.com/amazonlinux/container-images/blob/03d54f8c4d522bf712cffd6c8f9aafba0a875e78/Dockerfile)
* [`2.0.20200722.0-with-sources`, `2-with-sources`, `with-sources`](https://github.com/amazonlinux/container-images/blob/1e7349845e029a2e6afe6dc473ef17d052e3546f/Dockerfile)
* [`2018.03.0.20200602.1`, `2018.03`, `1`](https://github.com/amazonlinux/container-images/blob/f10932e08c75457eeb372bf1cc47ea2a4b8e98c8/Dockerfile)
* [`2018.03.0.20200602.1-with-sources`, `2018.03-with-sources`, `1-with-sources`](https://github.com/amazonlinux/container-images/blob/8c9ee491689d901aa72719be0ec12087a5fa8faf/Dockerfile)

## What is Amazon Linux?

Amazon Linux is provided by Amazon Web Services (AWS). It is designed to provide a stable, secure, and high-performance execution environment for applications running on Amazon EC2. The full distribution includes packages that enable easy integration with AWS, including launch configuration tools and many popular AWS libraries and tools. AWS provides ongoing security and maintenance updates to all instances running Amazon Linux.

The Amazon Linux container image contains a minimal set of packages. To install additional packages, [use `yum`](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/managing-software.html).

AWS provides two versions of Amazon Linux: [Amazon Linux 2](https://aws.amazon.com/amazon-linux-2/) and [Amazon Linux AMI](https://aws.amazon.com/amazon-linux-ami/).

For information on security updates for Amazon Linux, please refer to [Amazon Linux 2 Security Advisories](https://alas.aws.amazon.com/alas2.html) and [Amazon Linux AMI Security Advisories](https://alas.aws.amazon.com/). Note that Docker Hub's vulnerability scanning for Amazon Linux is currently based on RPM versions, which does not reflect the state of backported patches for vulnerabilities.

## Where can I run Amazon Linux container images?

You can run Amazon Linux container images in any Docker based environment. Examples include, your laptop, in AWS EC2 instances, and ECS clusters.

## License

Amazon Linux is available under the [GNU General Public License, version 2.0](https://github.com/aws/amazon-linux-docker-images/blob/master/LICENSE). Individual software packages are available under their own licenses; run `rpm -qi [package name]` or check `/usr/share/doc/[package name]-*` and `/usr/share/licenses/[package name]-*` for details.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `amazonlinux/` directory](https://github.com/docker-library/repo-info/tree/master/repos/amazonlinux).

## Security

For information on security updates for Amazon Linux, please refer to [Amazon Linux 2 Security Advisories](https://alas.aws.amazon.com/alas2.html) and [Amazon Linux AMI Security Advisories](https://alas.aws.amazon.com/). Note that Docker Hub's vulnerability scanning for Amazon Linux is currently based on RPM versions, which does not reflect the state of backported patches for vulnerabilities.
```

**AWS CLI**  
The following is how you would format the screenshot above using the AWS CLI\.

```
## Quick reference\n\nMaintained by: [the Amazon Linux Team](https://github.com/aws/amazon-linux-docker-images)\n\nWhere to get help: [the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://dockr.ly/slack), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)\n\n## Supported tags and respective `dockerfile` links\n\n* [`2.0.20200722.0`, `2`, `latest`](https://github.com/amazonlinux/container-images/blob/03d54f8c4d522bf712cffd6c8f9aafba0a875e78/Dockerfile)\n* [`2.0.20200722.0-with-sources`, `2-with-sources`, `with-sources`](https://github.com/amazonlinux/container-images/blob/1e7349845e029a2e6afe6dc473ef17d052e3546f/Dockerfile)\n* [`2018.03.0.20200602.1`, `2018.03`, `1`](https://github.com/amazonlinux/container-images/blob/f10932e08c75457eeb372bf1cc47ea2a4b8e98c8/Dockerfile)\n* [`2018.03.0.20200602.1-with-sources`, `2018.03-with-sources`, `1-with-sources`](https://github.com/amazonlinux/container-images/blob/8c9ee491689d901aa72719be0ec12087a5fa8faf/Dockerfile)\n\n## What is Amazon Linux?\n\nAmazon Linux is provided by Amazon Web Services (AWS). It is designed to provide a stable, secure, and high-performance execution environment for applications running on Amazon EC2. The full distribution includes packages that enable easy integration with AWS, including launch configuration tools and many popular AWS libraries and tools. AWS provides ongoing security and maintenance updates to all instances running Amazon Linux.\n\nThe Amazon Linux container image contains a minimal set of packages. To install additional packages, [use `yum`](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/managing-software.html).\n\nAWS provides two versions of Amazon Linux: [Amazon Linux 2](https://aws.amazon.com/amazon-linux-2/) and [Amazon Linux AMI](https://aws.amazon.com/amazon-linux-ami/).\n\nFor information on security updates for Amazon Linux, please refer to [Amazon Linux 2 Security Advisories](https://alas.aws.amazon.com/alas2.html) and [Amazon Linux AMI Security Advisories](https://alas.aws.amazon.com/). Note that Docker Hub's vulnerability scanning for Amazon Linux is currently based on RPM versions, which does not reflect the state of backported patches for vulnerabilities.\n\n## Where can I run Amazon Linux container images?\n\nYou can run Amazon Linux container images in any Docker based environment. Examples include, your laptop, in AWS EC2 instances, and ECS clusters.\n\n## License\n\nAmazon Linux is available under the [GNU General Public License, version 2.0](https://github.com/aws/amazon-linux-docker-images/blob/master/LICENSE). Individual software packages are available under their own licenses; run `rpm -qi [package name]` or check `/usr/share/doc/[package name]-*` and `/usr/share/licenses/[package name]-*` for details.\n\nAs with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).\n\nSome additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `amazonlinux/` directory](https://github.com/docker-library/repo-info/tree/master/repos/amazonlinux).\n\n## Security\n\nFor information on security updates for Amazon Linux, please refer to [Amazon Linux 2 Security Advisories](https://alas.aws.amazon.com/alas2.html) and [Amazon Linux AMI Security Advisories](https://alas.aws.amazon.com/). Note that Docker Hub's vulnerability scanning for Amazon Linux is currently based on RPM versions, which does not reflect the state of backported patches for vulnerabilities.
```

### Example: Full **Usage** description<a name="example-usagetext"></a>

The following screenshot from the Amazon ECR Public Gallery displays how an **Usage** section could be constructed\. We show how to format this text using both the AWS Management Console and the AWS CLI\.

![\[Example - Repository Usage\]](http://docs.aws.amazon.com/AmazonECR/latest/public/images/catalog-data-usage.png)

**AWS Management Console**  
The following is how you would format the screenshot above using the console\.

```
## Supported architectures

amd64, arm64v8

## Where can I run Amazon Linux container images?

You can run Amazon Linux container images in any Docker based environment. Examples include, your laptop, in AWS EC2 instances, and ECS clusters.

## How do I install a software package from Extras repository in Amazon Linux 2?

Available packages can be listed with the `amazon-linux-extras` command. Packages can be installed with the `amazon-linux-extras install <package>` command. Example: `amazon-linux-extras install rust1`

## Will updates be available for Amazon Linux containers?

Similar to the Amazon Linux images for AWS EC2 and on-premises use, Amazon Linux container images will get ongoing updates from Amazon in the form of security updates, bug fix updates, and other enhancements. Security bulletins for Amazon Linux are available at https://alas.aws.amazon.com/

## Will AWS support the current version of Amazon Linux going forward?

Yes; in order to avoid any disruption to your existing applications and to facilitate migration to Amazon Linux 2, AWS will provide regular security updates for Amazon Linux 2018.03 AMI and container image for 2 years after the final LTS build is announced. You can also use all your existing support channels such as AWS Premium Support and Amazon Linux Discussion Forum to continue to submit support requests.
```

**AWS CLI**  
The following is how you would format the screenshot above using the AWS CLI\.

```
## Supported architectures\n\namd64, arm64v8\n\n## Where can I run Amazon Linux container images?\n\nYou can run Amazon Linux container images in any Docker based environment. Examples include, your laptop, in AWS EC2 instances, and ECS clusters.\n\n## How do I install a software package from Extras repository in Amazon Linux 2?\n\nAvailable packages can be listed with the `amazon-linux-extras` command. Packages can be installed with the `amazon-linux-extras install <package>` command. Example: `amazon-linux-extras install rust1`\n\n## Will updates be available for Amazon Linux containers?\n\nSimilar to the Amazon Linux images for AWS EC2 and on-premises use, Amazon Linux container images will get ongoing updates from Amazon in the form of security updates, bug fix updates, and other enhancements. Security bulletins for Amazon Linux are available at https://alas.aws.amazon.com/\n\n## Will AWS support the current version of Amazon Linux going forward?\n\nYes; in order to avoid any disruption to your existing applications and to facilitate migration to Amazon Linux 2, AWS will provide regular security updates for Amazon Linux 2018.03 AMI and container image for 2 years after the final LTS build is announced. You can also use all your existing support channels such as AWS Premium Support and Amazon Linux Discussion Forum to continue to submit support requests.
```