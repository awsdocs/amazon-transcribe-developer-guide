# Amazon Transcribe identity\-based policy examples<a name="security_iam_id-based-policy-examples"></a>

By default, IAM users and roles don't have permission to create or modify Amazon Transcribe resources\. They also can't perform tasks using the AWS Management Console, AWS CLI, or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform specific API operations on the resources that they need\. The administrator must then attach those policies to the IAM users or groups that require those permissions\.

To learn how to create an IAM identity\-based policy using these example JSON policy documents, see [Creating policies on the JSON tab](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-json-editor) in the *IAM User Guide*\.

**Topics**
+ [Policy best practices](#security_iam_service-with-iam-policy-best-practices)
+ [Using the Amazon Transcribe console](#security_iam_id-based-policy-examples-console)
+ [AWS managed \(predefined\) policies for Amazon Transcribe](#auth-managed-policies)
+ [Permissions required for IAM user roles](#auth-role-iam-user)
+ [Permissions required for Amazon S3 encryption keys](#auth-role-kms-key)
+ [Allow users to view their own permissions](#security_iam_id-based-policy-examples-view-own-permissions)

## Policy best practices<a name="security_iam_service-with-iam-policy-best-practices"></a>

Identity\-based policies are very powerful\. They determine whether someone can create, access, or delete Amazon Transcribe resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get started using AWS managed policies** – To start using Amazon Transcribe quickly, use AWS managed policies to give your employees the permissions they need\. These policies are already available in your account and are maintained and updated by AWS\. For more information, see [Get started using permissions with AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-use-aws-defined-policies) in the *IAM User Guide*\.
+ **Grant least privilege** – When you create custom policies, grant only the permissions required to perform a task\. Start with a minimum set of permissions and grant additional permissions as necessary\. Doing so is more secure than starting with permissions that are too lenient and then trying to tighten them later\. For more information, see [Grant least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) in the *IAM User Guide*\.
+ **Enable MFA for sensitive operations** – For extra security, require IAM users to use multi\-factor authentication \(MFA\) to access sensitive resources or API operations\. For more information, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.
+ **Use policy conditions for extra security** – To the extent that it's practical, define the conditions under which your identity\-based policies allow access to a resource\. For example, you can write conditions to specify a range of allowable IP addresses that a request must come from\. You can also write conditions to allow requests only within a specified date or time range, or to require the use of SSL or MFA\. For more information, see [IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

## Using the Amazon Transcribe console<a name="security_iam_id-based-policy-examples-console"></a>

To access the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/), you must have a minimum set of permissions for the console\. These permissions must allow you to list and view details about the Amazon Transcribe resources in your AWS account\. If you create an identity\-based policy that applies permissions that are more restrictive than the minimum required permissions, the console won't function as intended for entities \(IAM users or roles\) with that policy\.

To ensure that those entities can use the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/), attach the following AWS managed policy to them\.

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

You don't need to allow minimum console permissions for users that are making calls only to the AWS CLI or the AWS API\. Instead, allow access to only the actions that match the API operation that you're trying to perform\. 

For more information, see [Adding Permissions to a User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html#users_change_permissions-add-console) in the *IAM User Guide*:

## AWS managed \(predefined\) policies for Amazon Transcribe<a name="auth-managed-policies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These policies are called AWS managed policies\. Managed policies make it easier for you to assign appropriate permissions to users, groups, and roles than if you had to write the policies yourself\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users, roles, and groups in your account, are specific to Amazon Transcribe:
+ **AmazonTranscribeReadOnly** – Grants read\-only access to Amazon Transcribe resources so that you can get and list transcription jobs and custom vocabularies\.
+ **AmazonTranscribeFullAccess** – Grants full access to create, read, update, delete, and run all Amazon Transcribe resources\. It also allows access to Amazon Simple Storage Service \(Amazon S3\) buckets with `transcribe` in the bucket name\.

**Note**  
You can review the managed permission policies by signing in to the IAM console and searching by policy name\. A search for "transcribe" returns both preceding policies \(*AmazonTranscribeReadOnly* and *AmazonTranscribeFullAccess*\)\.

You can also create your own custom IAM policies to allow permissions for Amazon Transcribe API actions\. You can attach these custom policies to the IAM users, roles, or groups that require those permissions\.

## Permissions required for IAM user roles<a name="auth-role-iam-user"></a>

When you create an IAM user to call Amazon Transcribe, the identity must have permission to access the S3 bucket and the AWS Key Management Service \(AWS KMS\) key used to encrypt the contents of the bucket, if you provided one\. 

The user must have the following IAM policy for decrypt permissions on the KMS Amazon Resource Name \(ARN\.\)

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": "arn:aws:kms:us-west-2:111122223333:key/KMS-Example-KeyId",
            "Effect": "Allow"
        }
    ]
}
```

The user's IAM policy must have Amazon S3 permissions to access the S3 bucket where audio files are stored and transcriptions are saved\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                        "s3:GetObject"
             ],
            "Resource": "arn:aws:s3:::your-s3-bucket/"
        }
    ]
}
```

## Permissions required for Amazon S3 encryption keys<a name="auth-role-kms-key"></a>

If you are using an AWS KMS key to encrypt an Amazon S3 bucket, include the following in the AWS KMS key policy\. This gives Amazon Transcribe access to the contents of the bucket\. 

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

For more information about allowing access to AWS KMS keys, see [ Allowing external AWS Accounts to access an AWS KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html#key-policy-modifying-external-accounts) in the *AWS KMS developer guide*\.

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