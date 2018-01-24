# Using Identity\-based Polices \(IAM Policies\) for Amazon Transcribe<a name="access-control-managing-permissions"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(users, groups, and roles\) and thereby grant permissions to perform Amazon Transcribe actions\. 

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

The policy has one statement that grants permission to use the `StartTranscriptionJob` action\.

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

## Permissions Required for Audio Transcription<a name="auth-role-permissions"></a>

To use the Amazon Transcribe `StartTranscriptionJob` operation, you must configure your S3 bucket to allow Amazon Transcribe to access objects\. Do this by adding a statement to the bucket policy of the S3 bucket\.

The following is an example S3 bucket policy statement:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "transcribe.amazonaws.com"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::bucket name/*"
        }
    ]
}
```

## Permissions Required for Amazon S3 Encryption Keys<a name="auth-role-cmk"></a>

If you are using an AWS Key Management Service key to encrypt an Amazon S3 bucket, you need to include the following in the AWS KMS key policy to allow Amazon Transcribe access to the contents of the bucket\. For more information about allowing access to customer master keys, see [ Allowing External AWS Accounts to Access a CMK](http://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html#key-policy-modifying-external-accounts) in the *AWS KMS Developer Guide*\.

```
{
      "Sid": "Allow-Transcribe",
      "Effect": "Allow",
      "Principal": {
        "Service": "transcribe.amazonaws.com”
      },
      "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:ReEncrypt*",
        "kms:GenerateDataKey*",
        "kms:DescribeKey"
      ],
      "Resource": "*"
    }
```