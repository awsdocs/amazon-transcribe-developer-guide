# Using Identity\-based Policies \(IAM Policies\) for Amazon Transcribe<a name="access-control-managing-permissions"></a>

The following identity\-based policies demonstrate how an account administrator can attach permissions policies to IAM identities \(users, groups, and roles\) to grant permissions to perform Amazon Transcribe actions\. 

**Important**  
Before you proceed, we recommend that you review [Overview of Managing Access Permissions to Amazon Transcribe Resources](access-control-overview.md)\. 

The following is the permissions policy required to use the Amazon Transcribe `StartTranscriptionJob` action:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "transcribe:StartTranscriptionJob"
             ],   
            "Resource": "*"
        }
    ]
}
```

The policy has one statement that grants permissions to use the `StartTranscriptionJob` action\.

The policy doesn't specify the `Principal` element because you don't specify the principal who gets the permission in an identity\-based policy\. When you attach a policy to a user, the user is the implicit principal\. When you attach a permissions policy to an IAM role, the principal identified in the role's trust policy gets the permissions\. 

For a table of Amazon Transcribe API actions and the resources that they apply to, see [Amazon Transcribe API Permissions: Actions, Resources, and Conditions Reference](asc-api-permissions-ref.md)\.

## Permissions Required to Use the Amazon Transcribe Console<a name="auth-console-permissions"></a>

To use the Amazon Transcribe console, you need to grant permissions for the actions shown in the following policy: 

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

The policy enables the user to call all of the Amazon Transcribe operations\.

## AWS Managed \(Predefined\) Policies for Amazon Transcribe<a name="auth-managed-policies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate which permissions are needed\. For more information, see [AWS Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to Amazon Transcribe:
+ **ReadOnly** — Grants read\-only access to Amazon Transcribe resources so that you can get and list transcription jobs and custom vocabularies\.
+ **FullAccess** — Grants full access to create, read, update, delete, and run all Amazon Transcribe resources\. It also allows access to S3 buckets with "transcribe" in the bucket name\.

**Note**  
You can review these permission policies by signing in to the IAM console and searching for specific policies\.

You can also create your own custom IAM policies to allow permissions for Amazon Transcribe API actions\. You can attach these custom policies to the IAM users or groups that require those permissions\.

## Permissions Required for IAM User Roles<a name="auth-role-iam-user"></a>

When you create an IAM user to call Amazon Transcribe, the identity must have permission for the S3 bucket and to the AWS Key Management Service \(AWS KMS\) key used to encrypt the contents of the bucket, if you provided one\. 

The user must have the following IAM policy to decrypt permissions on the KMS ARN:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": "KMS key ARN",
            "Effect": "Allow"
        }
    ]
}
```

The user's IAM policy must have Amazon S3 permissions to access the S3 bucket where audio files are stored and transcriptions are saved:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                        “s3:GetObject”,
             ],
            "Resource": "S3 bucket location"
        }
    ]
}
```

## Permissions Required for Amazon S3 Encryption Keys<a name="auth-role-cmk"></a>

If you are using an AWS Key Management Service key to encrypt an Amazon S3 bucket, include the following in the AWS KMS key policy\. This allows Amazon Transcribe access to the contents of the bucket\. For more information about allowing access to customer master keys, see [ Allowing External AWS Accounts to Access a CMK](http://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html#key-policy-modifying-external-accounts) in the *AWS KMS Developer Guide*\.

```
{
   "Sid": "Allow-Transcribe",
   "Effect": "Allow",
   "Principal": {
     "AWS": "arn:aws:iam::account id:root",
   },
   "Action": [
     "kms:Decrypt"
   ],
   "Resource": "KMS key ARN"
}
```