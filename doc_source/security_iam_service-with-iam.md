# How Amazon Transcribe Works with IAM<a name="security_iam_service-with-iam"></a>

Before you use IAM to manage access to Amazon Transcribe, you should understand which IAM features are available to use with Amazon Transcribe\. To get a high\-level view of how Amazon Transcribe and other AWS services work with IAM, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

**Topics**
+ [Amazon Transcribe Identity\-Based Policies](#security_iam_service-with-iam-id-based-policies)
+ [Amazon Transcribe IAM Roles](#security_iam_service-with-iam-roles)

## Amazon Transcribe Identity\-Based Policies<a name="security_iam_service-with-iam-id-based-policies"></a>

With IAM identity\-based policies, you can specify allowed or denied actions and resources and the conditions under which actions are allowed or denied\. Amazon Transcribe supports specific actions, resources, and condition keys\. To learn about all of the elements that you use in a JSON policy, see [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *IAM User Guide*\.

### Actions<a name="security_iam_service-with-iam-id-based-policies-actions"></a>

The `Action` element of an IAM identity\-based policy describes the specific action or actions that will be allowed or denied by the policy\. Policy actions usually have the same name as the associated AWS API operation\. The action is used in a policy to grant permissions to perform the associated operation\. 

Policy actions in Amazon Transcribe use the following prefix before the action: `transcribe:`\. For example, to grant someone permission to run an Amazon EC2 instance with the Amazon Transcribe `StartTranscriptionJob` API operation, you include the `transcribe:StartTranscriptionJob` action in their policy\. Policy statements must include either an `Action` or `NotAction` element\. Amazon Transcribe defines actions that describe tasks that you can perform with this service\.

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

### Resources<a name="security_iam_service-with-iam-id-based-policies-resources"></a>

Amazon Transcribe doesn't support specifying resource ARNs in a policy\.

#### Condition Keys<a name="security_iam_service-with-iam-id-based-policies-conditionkeys"></a>

Amazon Transcribe doesn't provide service\-specific condition keys, but it does support using some global condition keys\. For all AWS global condition keys, see [AWS Global Condition Context Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.

#### Examples<a name="security_iam_service-with-iam-id-based-policies-examples"></a>



For examples of Amazon Transcribe identity\-based policies, see [Amazon Transcribe Identity\-Based Policy Examples](security_iam_id-based-policy-examples.md)\.

### Amazon Transcribe Resource\-Based Policies<a name="security_iam_service-with-iam-resource-based-policies"></a>

Amazon Transcribe doesn't support resource\-based policies\.

## Amazon Transcribe IAM Roles<a name="security_iam_service-with-iam-roles"></a>

An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an entity within your AWS account that has specific permissions\.

### Using Temporary Credentials with Amazon Transcribe<a name="security_iam_service-with-iam-roles-tempcreds"></a>

You can use temporary credentials to sign in with federation, to assume an IAM role, or to assume a cross\-account role\. You obtain temporary security credentials by calling AWS Security Token Service \(AWS STS\) API operations, such as [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) or [GetFederationToken](https://docs.aws.amazon.com/STS/latest/APIReference/API_GetFederationToken.html)\. 

Amazon Transcribe supports using temporary credentials\. 

### Service\-Linked Roles<a name="security_iam_service-with-iam-roles-service-linked"></a>

[Service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role) allow AWS services to access resources in other services to complete an action on your behalf\. Service\-linked roles appear in your IAM account and are owned by the service\. An IAM administrator can view, but can't edit, the permissions for service\-linked roles\.

Amazon Transcribe doesn't support service\-linked roles\.

### Service Roles<a name="security_iam_service-with-iam-roles-service"></a>

You can allow a service to assume a [service role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-role) on your behalf\. This role allows the service to access resources in other services to complete an action on your behalf\. Service roles appear in your IAM account and are owned by the account\. This means that an IAM administrator can change the permissions for this role\. However, doing so might prevent the service from functioning as expected\.

Amazon Transcribe doesn't support service roles\. 