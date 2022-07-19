# Set up an AWS account and create an administrator user<a name="setting-up-med"></a>

Before you use Amazon Transcribe Medical for the first time, complete the following tasks:

1. [Sign up for Amazon Web Services](#setting-up-signup-med)

1. [Create an IAM user](#setting-up-iam-med)

## Sign up for Amazon Web Services<a name="setting-up-signup-med"></a>

When you sign up for Amazon Web Services, your AWS account is automatically signed up for all AWS services, including Amazon Transcribe Medical\. You are charged only for the services that you use\.

With Amazon Transcribe Medical, you pay only for the resources that you use\. If you are a new AWS customer, you can get started with Amazon Transcribe Medical for free\. For more information, see [AWS Free Usage Tier](http://aws.amazon.com/free/)\.

If you already have an AWS account, skip to the next section\. 

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

Record your AWS account ID because you'll need it for the next task\.

## Create an IAM user<a name="setting-up-iam-med"></a>

Services in AWS, such as Amazon Transcribe Medical, require that you provide credentials when you access them\. This allows the service to determine whether you have permissions to access the service's resources\. 

We strongly recommend that you access AWS using AWS Identity and Access Management \(IAM\), not the credentials for your AWS account\. To use IAM to access AWS, create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user\. You can then access AWS using a special URL and the IAM user's credentials\.

The Getting Started exercises in this guide assume that you have a user with administrator privileges, `adminuser`\. 

**To create an administrator user and sign in to the AWS Management Console**

1. Create an administrator user called `adminuser` in your AWS account\. For instructions, see [Creating Your First IAM User and Administrators Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

1. Sign in to the AWS Management Console using a special URL\. For more information, see [How Users Sign In to Your Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_how-users-sign-in.html) in the *IAM User Guide*\.

For more information about IAM, see the following:
+ [AWS Identity and Access Management \(IAM\)](https://aws.amazon.com/iam/)
+ [Getting started](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html)
+ [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)

## Next step<a name="setting-up-next-step-2-med"></a>

To get started with medical transcription using the AWS Management Console, see [Getting Started \(AWS Management Console\)](getting-started-med-console.md)\.