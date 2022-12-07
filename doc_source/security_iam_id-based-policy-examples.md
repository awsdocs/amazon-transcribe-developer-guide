# Amazon Transcribe identity\-based policy examples<a name="security_iam_id-based-policy-examples"></a>

By default, users and roles don't have permission to create or modify Amazon Transcribe resources\. They also can't perform tasks by using the AWS Management Console, AWS Command Line Interface \(AWS CLI\), or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform actions on the resources that they need\. The administrator must then attach those policies for users that require them\.

To learn how to create an IAM identity\-based policy by using these example JSON policy documents, see [Creating IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) in the *IAM User Guide*\.

For details about actions and resource types defined by Amazon Transcribe, including the format of the ARNs for each of the resource types, see [Actions, resources, and condition keys for Amazon Transcribe](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazontranscribe.html) in the *Service Authorization Reference*\.

**Topics**
+ [Policy best practices](#security_iam_service-with-iam-policy-best-practices)
+ [Using the AWS Management Console](#security_iam_id-based-policy-examples-console)
+ [AWS\-managed \(predefined\) policies for Amazon Transcribe](#auth-managed-policies)
+ [Permissions required for IAM user roles](#auth-role-iam-user)
+ [Permissions required for Amazon S3 encryption keys](#auth-role-kms-key)
+ [Allow users to view their own permissions](#security_iam_id-based-policy-examples-view-own-permissions)
+ [AWS KMS encryption context policy](#kms-context-policy)
+ [Confused deputy prevention policy](#confused-deputy-policy)
+ [Viewing transcription jobs based on tags](#tagging-transcription-policy)

## Policy best practices<a name="security_iam_service-with-iam-policy-best-practices"></a>

Identity\-based policies determine whether someone can create, access, or delete Amazon Transcribe resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get started with AWS managed policies and move toward least\-privilege permissions** – To get started granting permissions to your users and workloads, use the *AWS managed policies* that grant permissions for many common use cases\. They are available in your AWS account\. We recommend that you reduce permissions further by defining AWS customer managed policies that are specific to your use cases\. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) or [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.
+ **Apply least\-privilege permissions** – When you set permissions with IAM policies, grant only the permissions required to perform a task\. You do this by defining the actions that can be taken on specific resources under specific conditions, also known as *least\-privilege permissions*\. For more information about using IAM to apply permissions, see [ Policies and permissions in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\.
+ **Use conditions in IAM policies to further restrict access** – You can add a condition to your policies to limit access to actions and resources\. For example, you can write a policy condition to specify that all requests must be sent using SSL\. You can also use conditions to grant access to service actions if they are used through a specific AWS service, such as AWS CloudFormation\. For more information, see [ IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.
+ **Use IAM Access Analyzer to validate your IAM policies to ensure secure and functional permissions** – IAM Access Analyzer validates new and existing policies so that the policies adhere to the IAM policy language \(JSON\) and IAM best practices\. IAM Access Analyzer provides more than 100 policy checks and actionable recommendations to help you author secure and functional policies\. For more information, see [IAM Access Analyzer policy validation](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-policy-validation.html) in the *IAM User Guide*\.
+ **Require multi\-factor authentication \(MFA\)** – If you have a scenario that requires IAM users or root users in your account, turn on MFA for additional security\. To require MFA when API operations are called, add MFA conditions to your policies\. For more information, see [ Configuring MFA\-protected API access](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_configure-api-require.html) in the *IAM User Guide*\.

For more information about best practices in IAM, see [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

## Using the AWS Management Console<a name="security_iam_id-based-policy-examples-console"></a>

To access the Amazon Transcribe console, you must have a minimum set of permissions\. These permissions must allow you to list and view details about the Amazon Transcribe resources in your AWS account\. If you create an identity\-based policy that is more restrictive than the minimum required permissions, the console won't function as intended for entities \(users or roles\) with that policy\.

You don't need to allow minimum console permissions for users that are making calls only to the AWS CLI or the AWS API\. Instead, allow access to only the actions that match the API operation that you're trying to perform\.

To ensure that an entity \(users and roles\) can use the [AWS Management Console](https://console.aws.amazon.com/transcribe/), attach the following AWS\-managed policy to them\. For more information, see [Adding Permissions to a User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html#users_change_permissions-add-console) in the *AWS Identity and Access Management User Guide*\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "transcribe:*"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ]
}
```

## AWS\-managed \(predefined\) policies for Amazon Transcribe<a name="auth-managed-policies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These policies are called AWS managed policies\. Managed policies make it easier for you to assign appropriate permissions to users, groups, and roles than if you had to write the policies yourself\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *AWS Identity and Access Management User Guide*\.

The following AWS\-managed policies, which you can attach to entities in your AWS account, are specific to Amazon Transcribe:
+ **AmazonTranscribeReadOnly**: Grants read\-only access to Amazon Transcribe resources so that you can get and list transcription jobs and custom vocabularies\.
+ **AmazonTranscribeFullAccess**: Grants full access to create, read, update, delete, and run all Amazon Transcribe resources\. It also allows access to Amazon S3 buckets with `transcribe` in the bucket name\.

**Note**  
You can review the managed permission policies by signing in to the IAM AWS Management Console and searching by policy name\. A search for "transcribe" returns both policies listed above \(*AmazonTranscribeReadOnly* and *AmazonTranscribeFullAccess*\)\.

You can also create your own custom IAM policies to allow permissions for Amazon Transcribe API actions\. You can attach these custom policies to the entities that require those permissions\.

## Permissions required for IAM user roles<a name="auth-role-iam-user"></a>

When you create an IAM user to call Amazon Transcribe, the identity must have permission to access the Amazon S3 bucket and the KMS key used to encrypt the contents of the bucket, if you provided one\. 

### Trust policies<a name="trust-policy"></a>

The IAM entity you use to make your transcription request must have a trust policy that enables Amazon Transcribe to assume that role\. Use the following Amazon Transcribe trust policy\. Note that if you're making a real\-time Call Analytics request with post\-call analytics enabled, you must use 'Trust policy for real\-time Call Analytics'\.

**Trust policy for Amazon Transcribe**

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "transcribe.amazonaws.com"
        ]
      },
      "Action": [
        "sts:AssumeRole"
      ],      
      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": "111122223333"
        },
        "StringLike": {
          "aws:SourceArn": "arn:aws:transcribe:us-west-2:111122223333:*"
        }
      }
    }
  ]
}
```

**Trust policy for real\-time Call Analytics**

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "transcribe.streaming.amazonaws.com"
        ]
      },
      "Action": [
        "sts:AssumeRole"
      ],      
      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": "111122223333"
        },
        "StringLike": {
          "aws:SourceArn": "arn:aws:transcribe:us-west-2:111122223333:*"
        }
      }
    }
  ]
}
```

### Amazon S3 input bucket policy<a name="input-bucket"></a>

The following policy gives an IAM role permission to access files from the specified input bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": [
            "s3:GetObject",
            "s3:ListBucket"
        ],
        "Resource": [
            "arn:aws:s3:::DOC-EXAMPLE-INPUT-BUCKET",
            "arn:aws:s3:::DOC-EXAMPLE-INPUT-BUCKET/*"
        ]
    }
}
```

### Amazon S3 output bucket policy<a name="output-bucket"></a>

The following policy gives an IAM role permission to write files to the specified output bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": [
            "arn:aws:s3:::DOC-EXAMPLE-OUTPUT-BUCKET/*"
        ]
    }
}
```

## Permissions required for Amazon S3 encryption keys<a name="auth-role-kms-key"></a>

If you're using a KMS key to encrypt an Amazon S3 bucket, include the following in the KMS key policy\. This gives Amazon Transcribe access to the contents of the bucket\. For more information about allowing access to KMS keys, see [ Allowing external AWS accounts to access an KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html#key-policy-modifying-external-accounts) in the *AWS KMS Developer Guide*\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::111122223333:role/ExampleRole"
      },
      "Action": [
        "kms:Decrypt"
      ],
      "Resource": "arn:aws:kms:us-west-2:111122223333:key/KMS-Example-KeyId"
    }
  ]
}
```

## Allow users to view their own permissions<a name="security_iam_id-based-policy-examples-view-own-permissions"></a>

This example shows how you might create a policy that allows IAM users to view the inline and managed policies that are attached to their user identity\. This policy includes permissions to complete this action on the console or programmatically using the AWS CLI or AWS API\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ViewOwnUserInfo",
            "Effect": "Allow",
            "Action": [
                "iam:GetUserPolicy",
                "iam:ListGroupsForUser",
                "iam:ListAttachedUserPolicies",
                "iam:ListUserPolicies",
                "iam:GetUser"
            ],
            "Resource": ["arn:aws:iam::*:user/${aws:username}"]
        },
        {
            "Sid": "NavigateInConsole",
            "Effect": "Allow",
            "Action": [
                "iam:GetGroupPolicy",
                "iam:GetPolicyVersion",
                "iam:GetPolicy",
                "iam:ListAttachedGroupPolicies",
                "iam:ListGroupPolicies",
                "iam:ListPolicyVersions",
                "iam:ListPolicies",
                "iam:ListUsers"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS KMS encryption context policy<a name="kms-context-policy"></a>

The following policy grants the IAM role “`ExampleRole`” permission to use the AWS KMS *Decrypt* and *Encrypt* operations for this particular KMS key\. This policy works **only** for requests with at least one encryption context pair, in this case "`color:indig0Blu3`”\. For more information on AWS KMS encryption context, see [AWS KMS encryption context](data-encryption.md#kms-context)\.

```
{
  "Version": "2012-10-17",
  "Statement": [
      {
          "Effect": "Allow",
          "Principal": {
              "AWS": "arn:aws:iam::111122223333:role/ExampleRole"
          },
          "Action": [
              "kms:Decrypt",
              "kms:DescribeKey",
              "kms:Encrypt",
              "kms:GenerateDataKey*",
              "kms:ReEncrypt*"
          ],
          "Resource": "*",
          "Condition": {
              "StringEquals": {
                  "kms:EncryptionContext:color":"indig0Blu3"
              }
           }
        }
   ]
}
```

## Confused deputy prevention policy<a name="confused-deputy-policy"></a>

Here's an example of an assume role policy that shows how you can use `aws:SourceArn` and `aws:SourceAccount` with Amazon Transcribe to prevent a confused deputy issue\. For more information on confused deputy prevention, see [Cross\-service confused deputy prevention](security-iam-confused-deputy.md)\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "transcribe.amazonaws.com"
      },
      "Action": [
        "sts:AssumeRole",
      ],
      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": "111122223333"
        },
        "StringLike": {
          "aws:SourceArn": "arn:aws:transcribe:us-west-2:111122223333:*"
        }
      }
    }
  ]
}
```

## Viewing transcription jobs based on tags<a name="tagging-transcription-policy"></a>

You can use conditions in your identity\-based policy to control access to Amazon Transcribe resources based on tags\. This example shows how you might create a policy that allows viewing a transcription job\. However, permission is granted only if the transcription job tag `Owner` has the value of that user's user name\. This policy also grants the permissions necessary to complete this action using the AWS Management Console\.

You can attach this policy to the IAM users in your account\. If a user named `richard-roe` attempts to view a transcription job, the transcription job must be tagged `Owner=richard-roe` or `owner=richard-roe`\. Otherwise they are denied access\. The condition tag key `Owner` matches both `Owner` and `owner` because condition key names are not case\-sensitive\. For more information, see [IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

For more information on tagging in Amazon Transcribe, see [Tagging resources](tagging.md)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListTranscriptionJobsInConsole",
            "Effect": "Allow",
            "Action": "transcribe:ListTranscriptionJobs",
            "Resource": "*"
        },
        {
            "Sid": "ViewTranscriptionJobsIfOwner",
            "Effect": "Allow",
            "Action": "transcribe:GetTranscriptionJobs",
            "Resource": "arn:aws:transcribe:*:*:transcription-job/*",
            "Condition": {
                "StringEquals": {"aws:ResourceTag/Owner": "${aws:username}"}
            }
        }
    ]
}
```