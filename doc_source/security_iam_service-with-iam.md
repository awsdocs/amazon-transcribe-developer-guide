# How Amazon Transcribe works with IAM<a name="security_iam_service-with-iam"></a>

Before you use IAM to manage access to Amazon Transcribe, you should understand which IAM features are available to use with Amazon Transcribe\. To get a high\-level view of how Amazon Transcribe and other AWS services work with IAM, see [AWS services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

**Topics**
+ [Amazon Transcribe identity\-based policies](#security_iam_service-with-iam-id-based-policies)
+ [Amazon Transcribe IAM roles](#security_iam_service-with-iam-roles)

## Amazon Transcribe identity\-based policies<a name="security_iam_service-with-iam-id-based-policies"></a>

With IAM identity\-based policies, you can specify allowed or denied actions and resources and the conditions under which actions are allowed or denied\. Amazon Transcribe supports specific actions, resources, and condition keys\. To learn about all of the elements that you use in a JSON policy, see [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *IAM User Guide*\.

### Actions<a name="security_iam_service-with-iam-id-based-policies-actions"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Action` element of a JSON policy describes the actions that you can use to allow or deny access in a policy\. Policy actions usually have the same name as the associated AWS API operation\. There are some exceptions, such as *permission\-only actions* that don't have a matching API operation\. There are also some operations that require multiple actions in a policy\. These additional actions are called *dependent actions*\.

Include actions in a policy to grant permissions to perform the associated operation\.

Policy actions in Amazon Transcribe use the following prefix before the action: `transcribe:`\. For example, to grant someone permission to run an Amazon EC2 instance with the Amazon Transcribe [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API, you include the `transcribe:StartTranscriptionJob` action in their policy\. Policy statements must include either an `Action` or `NotAction` element\. Amazon Transcribe defines actions that describe tasks that you can perform with this service\.

To specify multiple actions in a single statement, separate them with commas as follows\.

```
"Action": [
      "transcribe:action1",
      "transcribe:action2"
```

You can specify multiple actions using wildcards \(\*\)\. For example, to specify all actions that begin with the word `List`, include the following action\.

```
"Action": "transcribe:List*"
```



To see a list of Amazon Transcribe actions, see [Actions Defined by Amazon Transcribe](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazontranscribe.html#amazontranscribe-actions-as-permissions) in the *IAM User Guide*\.

**Note**  
You can also control access to your resources using tags\. For information on tag\-based access control, see [Controlling access to AWS resources using tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html)\.

### Resources<a name="security_iam_service-with-iam-id-based-policies-resources"></a>

Amazon Transcribe doesn't support specifying resource ARNs in a policy\.

#### Condition keys<a name="security_iam_service-with-iam-id-based-policies-conditionkeys"></a>

Use the `Condition` element \(or a `Condition` *block*\) to specify conditions in which a statement is in effect\. The `Condition` element is optional\. You can build conditional expressions that use [condition operators](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html), such as equals or less than, to match the condition in the policy with values in the request\.

If you specify multiple `Condition` elements in a statement, or multiple keys in a single `Condition` element, AWS evaluates them using a logical `AND` operation\. If you specify multiple values for a single condition key, AWS evaluates the condition using a logical `OR` operation\. All of the conditions must be met before the statement's permissions are granted\.

You can also use placeholder variables when you specify conditions\. For example, you can grant an IAM user permission to access a resource only if it is tagged with their IAM user name\. For more information, see [IAM policy elements: variables and tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_variables.html) in the *IAM user guide*\.

Amazon Transcribe defines its own set of condition keys and also supports using some global condition keys\. For a list of all AWS global condition keys, see [AWS global condition context keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.

The following table lists the Amazon Transcribe condition keys that apply to Amazon Transcribe resources\. You can include these keys in the `Condition` element in an IAM permissions policy\.


| Amazon Transcribe condition key | Description | Value type | Action | 
| --- | --- | --- | --- | 
| transcribe:OutputBucketName | Filters access by the output bucket used to start a transcription job\. | String | [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) | 
| transcribe:OutputEncryptionKMSKeyId | Filters access by the KMS key used to start a transcription job\. | String | [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) | 
| transcribe:Outputkey | Filters access by the output key used to start a transcription job\. | String | [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) | 

For examples of how you can use condition keys to control access to the resources of Amazon Transcribe, see the following\.

If you want your users to always use a specific output bucket when they use the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API, you can use the following policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "transcribe:StartTranscriptionJob",
                  ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "transcribe:OutputBucketName": "DOC-EXAMPLE-BUCKET"
                }
            }
        }
    ]
}
```

If you want users to always use a AWS Key Management Service \(KMS\) key when they use the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API, you can use the following policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "transcribe:StartTranscriptionJob",
                  ],
            "Resource": "*",
            "Condition": {
                "Null": {
                    "transcribe:OutputEncryptionKMSKeyId": "false"
                }
            }
        }
    ]
}
```

For information on AWS KMS keys, see [Key management](key-management.md)\.

If you want your users to always use a specific output key when they use the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API, you can use the following policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "transcribe:StartTranscriptionJob",
                  ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "transcribe:Outputkey": "DOC-EXAMPLE-BUCKET/prefix"
                }
            }
        }
    ]
}
```

For more information, see the `OutputKey` parameter description of the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API\.

#### Examples<a name="security_iam_service-with-iam-id-based-policies-examples"></a>



For examples of Amazon Transcribe identity\-based policies, see [Amazon Transcribe identity\-based policy examples](security_iam_id-based-policy-examples.md)\.

#### <a name="transcribe-"></a>

### Amazon Transcribe resource\-based policies<a name="security_iam_service-with-iam-resource-based-policies"></a>

Amazon Transcribe doesn't support resource\-based policies\.

## Amazon Transcribe IAM roles<a name="security_iam_service-with-iam-roles"></a>

An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an entity within your AWS account that has specific permissions\.

### Using temporary credentials with Amazon Transcribe<a name="security_iam_service-with-iam-roles-tempcreds"></a>

You can use temporary credentials to sign in with federation, to assume an IAM role, or to assume a cross\-account role\. You obtain temporary security credentials by calling AWS Security Token Service \(AWS STS\) APIs, such as [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) or [GetFederationToken](https://docs.aws.amazon.com/STS/latest/APIReference/API_GetFederationToken.html)\. 

Amazon Transcribe supports using temporary credentials\. 

### Service\-linked roles<a name="security_iam_service-with-iam-roles-service-linked"></a>

[Service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role) allow AWS services to access resources in other services to complete an action on your behalf\. Service\-linked roles appear in your IAM account and are owned by the service\. An IAM administrator can view, but can't edit, the permissions for service\-linked roles\.

Amazon Transcribe doesn't support service\-linked roles\.

### Service roles<a name="security_iam_service-with-iam-roles-service"></a>

You can allow a service to assume a [service role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-role) on your behalf\. This role allows the service to access resources in other services to complete an action on your behalf\. Service roles appear in your IAM account and are owned by the account\. This means that an IAM administrator can change the permissions for this role\. However, doing so might prevent the service from functioning as expected\.

Refer to [Cross\-service confused deputy prevention](security-iam-confused-deputy.md) to learn about preventing unwanted services from assuming roles and performing actions with Amazon Transcribe\.