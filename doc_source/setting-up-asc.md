# Step 1: Set up an AWS Account and Create an Administrator User<a name="setting-up-asc"></a>

Before you use Amazon Transcribe for the first time, complete the following tasks:

1. [Sign up for AWS](#setting-up-asc-signup)

1. [Create an IAM User](#setting-up-asc-iam)

## Sign up for AWS<a name="setting-up-asc-signup"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all AWS services, including Amazon Transcribe\. You are charged only for the services that you use\.

With Amazon Transcribe, you pay only for the resources that you use\. If you are a new AWS customer, you can get started with Amazon Transcribe for free\. For more information, see [AWS Free Usage Tier](https://aws.amazon.com//free/)\.

If you already have an AWS account, skip to the next section\. 

**To create an AWS account**

1. Open [https://aws\.amazon\.com/](https://aws.amazon.com/), and then choose **Create an AWS Account**\.
**Note**  
This might be unavailable in your browser if you previously signed into the AWS Management Console\. In that case, choose **Sign In to the Console**, and then choose **Create a new AWS account**\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a PIN using the phone keypad\.

Record your AWS account ID because you'll need it for the next task\.

## Create an IAM User<a name="setting-up-asc-iam"></a>

Services in AWS, such as Amazon Transcribe, require that you provide credentials when you access them\. This allows the service to determine whether you have permissions to access the service's resources\. 

We strongly recommend that you access AWS using AWS Identity and Access Management \(IAM\), not the credentials for your AWS account\. To use IAM to access AWS, create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user\. You can then access AWS using a special URL and the IAM user's credentials\.

The Getting Started exercises in this guide assume that you have a user with administrator privileges, `adminuser`\. 

**To create an administrator user and sign in to the console**

1. Create an administrator user called `adminuser` in your AWS account\. For instructions, see [Creating Your First IAM User and Administrators Group](http://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

1. Sign in to the AWS Management Console using a special URL\. For more information, see [How Users Sign In to Your Account](http://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_how-users-sign-in.html) in the *IAM User Guide*\.

For more information about IAM, see the following:

+ [AWS Identity and Access Management \(IAM\)](https://aws.amazon.com/iam/)

+ [Getting Started](http://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html)

+ [IAM User Guide](http://docs.aws.amazon.com/IAM/latest/UserGuide/)

## Next Step<a name="setting-up-asc-next-step-2"></a>

[Step 2: Set up the AWS Command Line Interface \(AWS CLI\)](setup-asc-awscli.md)