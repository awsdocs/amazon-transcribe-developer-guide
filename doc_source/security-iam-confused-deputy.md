# Cross\-service confused deputy prevention<a name="security-iam-confused-deputy"></a>

A confused deputy is an entity \(a service or an account\) that is coerced by a different entity to perform an action\. This type of impersonation can happen cross\-account and cross\-service\.

To prevent confused deputies, AWS provides tools that help you protect your data for all services using service principals that have been given access to resources in your account\. This section focuses on cross\-service confused deputy prevention specific to Amazon Transcribe; however, you can learn more about this topic in the [ confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html) section of the IAM User Guide\.

To limit the permissions IAM gives to Amazon Transcribe to access your resources, we recommend using the global condition context keys [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) in your resource policies\. Note that if you use both of these global condition context keys, and the `aws:SourceArn` value contains the account ID, the `aws:SourceAccount` value and the account in the `aws:SourceArn` value must use the same account ID when used in the same policy statement\.

If you want only one resource to be associated with the cross\-service access, use `aws:SourceArn`\. If you want to associate any resource in that account with cross\-service access, use `aws:SourceAccount`\.

**Note**  
The most effective way to protect against the confused deputy problem is to use the `aws:SourceArn` global condition context key with the **full ARN** of the resource\. If you don’t know the full ARN, or if you're specifying multiple resources, use the `aws:SourceArn` global context condition key with wildcards \(`*`\) for the unknown portions of the ARN\. For example, `arn:aws:transcribe::123456789012:*`\.

Here's an example of an assume role policy that shows how you can use `aws:SourceArn` and `aws:SourceAccount` with Amazon Transcribe to prevent a confused deputy issue\.

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