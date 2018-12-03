# Amazon Transcribe API Permissions: Actions, Resources, and Conditions Reference<a name="asc-api-permissions-ref"></a>

Use the following table as a reference when setting up [Access Control](auth-and-access-control.md#access-control) and writing a permissions policy that you can attach to an IAM identity \(an identity\-based policy\)\. The list includes each Amazon Transcribe API operation, the corresponding action for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

To express conditions in your Amazon Transcribe policies, you can use AWS\-wide condition keys\. For a complete list of AWS\-wide keys, see [Available Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `transcribe:` prefix followed by the API operation name, for example, `transcribe:StartTranscriptionJob`\.

If you see an expand arrow \(**↗**\) in the upper\-right corner of the table, you can open the table in a new window\. To close the window, choose the close button \(**X**\) in the lower\-right corner\.


**Amazon Transcribe API and Required Permissions for Actions**  

| Amazon Transcribe API Operations | Required Permissions \(API Actions\) | Resources | 
| --- | --- | --- | 
| [CreateVocabulary](API_CreateVocabulary.md) | transcribe:CreateVocabulary | \* | 
| [DeleteVocabulary](API_DeleteVocabulary.md) | transcribe:DeleteVocabulary | \* | 
| [GetTranscriptionJob](API_GetTranscriptionJob.md) | transcribe:GetTranscriptionJob | \* | 
| [GetVocabulary](API_GetVocabulary.md) | transcribe:GetVocabulary | \* | 
| [ListTranscriptionJobs](API_ListTranscriptionJobs.md) | transcribe:ListTranscriptionJobs | \* | 
| [ListVocabularies](API_ListVocabularies.md) | transcribe:ListVocabularies | \* | 
| [StartTranscriptionJob](API_StartTranscriptionJob.md) | transcribe:StartTranscriptionJob | \* | 
| [UpdateVocabulary](API_UpdateVocabulary.md) | transcribe:UpdateVocabulary | \* | 