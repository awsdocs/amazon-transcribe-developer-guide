# Getting started with Amazon Transcribe<a name="getting-started"></a>

Before you can create transcriptions, you have a few prerequisites:
+ [Sign up for an AWS account](#getting-started-sign-up)
+ [Install the AWS CLI and SDK](#getting-started-api) \(if you're using the AWS Management Console for your transcriptions, you can skip this step\)
+ [Create an IAM user with administrator permissions](#getting-started-iam)
+ [Set up an S3 bucket](#getting-started-s3)

Once you complete these prerequisites, you're ready to transcribe\. Select your preferred transcription method from the following list to get started\.
+ [AWS CLI](getting-started-cli.md)
+ [AWS Management Console](getting-started-console.md)
+ [AWS SDK](getting-started-sdk.md)
+ [HTTP](getting-started-http-websocket.md)
+ [WebSockets](getting-started-http-websocket.md)

Because streaming using HTTP/2 and WebSockets is more complicated than the other transcription methods, we advise reviewing the [Setting up a streaming transcription](streaming-setting-up.md) section before getting started with these methods\.

## Signing up for an AWS account<a name="getting-started-sign-up"></a>

You can sign up for either a [free tier](http://aws.amazon.com/free/) account or a [paid account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html)\. Both options give you access to all AWS services\. The free tier has a trial period during which you can explore AWS services and get a feel for your usage\. Once your trial period expires, you can migrate to a paid account\. Fees are accrued on a pay\-as\-you\-use basis; see [Amazon Transcribe Pricing](http://aws.amazon.com/transcribe/pricing/) for details\.

**Tip**  
When setting up your account, make note of your AWS account ID because you need it to create an IAM user or group\.

## Installing the AWS CLI and SDK<a name="getting-started-api"></a>

To use the Amazon Transcribe API, you must first install the AWS CLI\. The current AWS CLI is version 2\. You can find installation instructions for [Linux](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html), [Mac](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html), [Windows](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html), and [Docker](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-docker.html) in the [AWS Command Line Interface User Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)\. 

Once you have the AWS CLI installed, you need to [configure](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) it for your security credentials and AWS Region\.

If you want to use Amazon Transcribe with an SDK, click on your preferred language for installation instructions:
+ [\.NET](https://docs.aws.amazon.com/sdk-for-net/v3/developer-guide/quick-start.html)
+ [C\+\+](https://docs.aws.amazon.com/sdk-for-cpp/v1/developer-guide/getting-started.html)
+ [Go](https://aws.github.io/aws-sdk-go-v2/docs/)
+ [Java V2](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/setup.html)
+ [JavaScript](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/getting-started.html)
+ [PHP V3](https://docs.aws.amazon.com/sdk-for-php/v3/developer-guide/getting-started_installation.html)
+ [Python \(Boto3\)](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/quickstart.html) — batch transcriptions only
+ [Python](https://github.com/awslabs/amazon-transcribe-streaming-sdk) — streaming transcriptions only
+ [Ruby V3](https://docs.aws.amazon.com/sdk-for-ruby/v3/developer-guide/setup-install.html)

## Creating an IAM user<a name="getting-started-iam"></a>

IAM, or Identity and Access Management, is a means of controlling which users can access which resources\. All AWS services use IAM credentials and it is best practice to use an IAM admin user to access your resources\. Using your AWS account root user credentials to access resources is **not** recommended\. To learn more about IAM, see [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

You can create an IAM admin user with the AWS Management Console or AWS CLI\. For instructions, see [Creating your first IAM admin user and user group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html)\. For information on signing in to your account using IAM user credentials, refer to [How IAM users sign in to your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_how-users-sign-in.html)\.

For CLI\-specific IAM instructions, see [Using an IAM role in the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-role.html)\.

## Creating an S3 bucket<a name="getting-started-s3"></a>

Amazon Simple Storage Service \(Amazon S3\) is a secure object storage service\. Amazon S3 stores your files \(called *objects*\) in containers \(called *buckets*\)\.

To run a batch transcription, you must first upload your media files into an S3 bucket\. If you don't specify an S3 bucket for your transcription output, Amazon Transcribe puts your transcript in a temporary AWS managed S3 bucket\. Transcription output in AWS managed buckets is automatically deleted after 90 days\.

Learn how to [Create your first S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) and [Upload an object to your bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/uploading-an-object-bucket.html)\.