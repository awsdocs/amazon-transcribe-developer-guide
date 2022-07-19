# Amazon Transcribe identity\-based policy examples<a name="security_iam_id-based-policy-examples"></a>

By default, IAM users and roles don't have permission to create or modify Amazon Transcribe resources\. They also can't perform tasks using the AWS Management Console, AWS CLI, or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform actions on the resources that they need\. The administrator must then attach those policies to the IAM users or groups that require those permissions\.

To learn how to create an IAM identity\-based policy using these example JSON policy documents, see [Creating IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) in the *IAM User Guide*\.

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

Identity\-based policies are very powerful\. They determine whether someone can create, access, or delete Amazon Transcribe resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get started using AWS managed policies** – To start using Amazon Transcribe quickly, use AWS managed policies to give your employees the permissions they need\. These policies are already available in your account and are maintained and updated by AWS\. For more information, see [Get started using permissions with AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-use-aws-defined-policies) in the *IAM User Guide*\.
+ **Grant least privilege** – When you create custom policies, grant only the permissions required to perform a task\. Start with a minimum set of permissions and grant additional permissions as necessary\. Doing so is more secure than starting with permissions that are too lenient and then trying to tighten them later\. For more information, see [Grant least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) in the *IAM User Guide*\.
+ **Enable MFA for sensitive operations** – For extra security, require IAM users to use multi\-factor authentication \(MFA\) to access sensitive resources or API operations\. For more information, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.
+ **Use policy conditions for extra security** – To the extent that it's practical, define the conditions under which your identity\-based policies allow access to a resource\. For example, you can write conditions to specify a range of allowable IP addresses that a request must come from\. You can also write conditions to allow requests only within a specified date or time range, or to require the use of SSL or MFA\. For more information, see [IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

## Using the AWS Management Console<a name="security_iam_id-based-policy-examples-console"></a>

To access the Amazon Transcribe console, you must have a minimum set of permissions\. These permissions must allow you to list and view details about the Amazon Transcribe resources in your AWS account\. If you create an identity\-based policy that is more restrictive than the minimum required permissions, the console won't function as intended for entities \(IAM users or roles\) with that policy\.

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

### Trust policy<a name="trust-policy"></a>

The IAM entity you use to make your transcription request must have a trust policy that enables Amazon Transcribe to assume that role\. Use the following trust policy\.

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
            "Action": "sts:AssumeRole"
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