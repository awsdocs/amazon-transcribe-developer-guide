# Overview of Managing Access Permissions to Amazon Transcribe Resources<a name="access-control-overview"></a>

Permissions to access an action are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) to manage access to actions\. 

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. We strongly recommend that you access AWS using IAM not the credentials for your AWS account\. To use IAM to access AWS, create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user\. You can then access AWS using a special URL and the IAM user's credentials\. For more information, see [IAM Best Practices](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions and the actions they get permissions for\.


+ [Managing Access to Actions](#access-control-manage-access-intro)
+ [Specifying Policy Elements: Resources, Actions, Effects, and Principals](#access-control-specify-asc-actions)
+ [Specifying Conditions in a Policy](#specifying-conditions)

## Managing Access to Actions<a name="access-control-manage-access-intro"></a>

A *permissions policy* describes who has access to what\. You have several options for creating permissions policies\.

**Note**  
This topic discusses using IAM in the context of Amazon Transcribe\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](http://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM polices\)\. Policies attached to a resource are referred to as *resource\-based* policies\. Amazon Transcribe supports only identity\-based policies\. 

### Identity\-Based Policies \(IAM Policies\)<a name="access-control-manage-access-intro-iam-policies"></a>

You can attach policies to IAM identities\. For example, you can do the following:

+ **Attach a permissions policy to a user or a group in your account**—To grant a user or a group of users permissions to call an Amazon Transcribe action, you can attach a permissions policy to a user or group that the user belongs to\.

+ **Attach a permissions policy to a role \(grant cross\-account permissions\)**—To grant cross\-account permissions, you can attach an identity\-based permissions policy to an IAM role\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. If you want to grant an AWS service permissions to assume the role, the principal in the trust policy can be an AWS service principal\.

  For more information about using IAM to delegate permissions, see [Access Management](http://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\.

For more information about using identity\-based policies with Amazon Transcribe, see [Using Identity\-based Polices \(IAM Policies\) for Amazon Transcribe](access-control-managing-permissions.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-Based Policies<a name="access-control-manage-access-intro-resource-policies"></a>

Other services, such as AWS Lambda, support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. Amazon Transcribe doesn't support resource\-based policies\. 

## Specifying Policy Elements: Resources, Actions, Effects, and Principals<a name="access-control-specify-asc-actions"></a>

Amazon Transcribe defines a set of API operations \(see [Actions](API_Operations.md)\)\. To grant permissions for these API operations, Amazon Transcribe defines a set of actions that you can specify in a policy\. 

The following are the most basic policy elements:

+ **Resource**—In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For Amazon Transcribe, the resource is always `*`\.

+ **Action**—You use action keywords to identify operations that you want to allow or deny\. For example, depending on the specified `Effect`, `transcribe:StartTranscriptionJob` either allows or denies the user permissions to perform the Amazon Transcribe `StartTranscriptionJob` operation\.

+ **Effect**—You specify the effect of the action that occurs when the user requests the specific action–this can be either allow or deny\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource\. You might do this to make sure that a user cannot access the resource, even if a different policy grants access\.

+ **Principal**—In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. 

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table of Amazon Transcribe API actions, see [Amazon Transcribe API Permissions: Actions, Resources, and Conditions Reference](asc-api-permissions-ref.md)\.

## Specifying Conditions in a Policy<a name="specifying-conditions"></a>

When you grant permissions, you use the IAM policy language to specify the conditions under which a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\. 

AWS provides a set of predefined condition keys for all AWS services that support IAM for access control\. For example, you can use the `aws:userid` condition key to require a specific AWS ID when requesting an action\. For more information and a complete list of AWS\-wide keys, see [Available Keys for Conditions](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
Condition keys are case\-sensitive\.

Amazon Transcribe does not provide additional condition keys\.