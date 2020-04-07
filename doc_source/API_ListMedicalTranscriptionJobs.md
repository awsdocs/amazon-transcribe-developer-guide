# ListMedicalTranscriptionJobs<a name="API_ListMedicalTranscriptionJobs"></a>

Lists medical transcription jobs with a specified status or substring that matches their names\.

## Request Syntax<a name="API_ListMedicalTranscriptionJobs_RequestSyntax"></a>

```
{
   "[JobNameContains](#transcribe-ListMedicalTranscriptionJobs-request-JobNameContains)": "string",
   "[MaxResults](#transcribe-ListMedicalTranscriptionJobs-request-MaxResults)": number,
   "[NextToken](#transcribe-ListMedicalTranscriptionJobs-request-NextToken)": "string",
   "[Status](#transcribe-ListMedicalTranscriptionJobs-request-Status)": "string"
}
```

## Request Parameters<a name="API_ListMedicalTranscriptionJobs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [JobNameContains](#API_ListMedicalTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListMedicalTranscriptionJobs-request-JobNameContains"></a>
When specified, the jobs returned in the list are limited to jobs whose name contains the specified string\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** [MaxResults](#API_ListMedicalTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListMedicalTranscriptionJobs-request-MaxResults"></a>
The maximum number of medical transcription jobs to return in the response\. IF there are fewer results in the list, this response contains only the actual results\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListMedicalTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListMedicalTranscriptionJobs-request-NextToken"></a>
If you a receive a truncated result in the previous request of `ListMedicalTranscriptionJobs`, include `NextToken` to fetch the next set of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

 ** [Status](#API_ListMedicalTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListMedicalTranscriptionJobs-request-Status"></a>
When specified, returns only medical transcription jobs with the specified status\. Jobs are ordered by creation date, with the newest jobs returned first\. If you don't specify a status, Amazon Transcribe Medical returns all transcription jobs ordered by creation date\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED`   
Required: No

## Response Syntax<a name="API_ListMedicalTranscriptionJobs_ResponseSyntax"></a>

```
{
   "[MedicalTranscriptionJobSummaries](#transcribe-ListMedicalTranscriptionJobs-response-MedicalTranscriptionJobSummaries)": [ 
      { 
         "[CompletionTime](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-CompletionTime)": number,
         "[CreationTime](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-CreationTime)": number,
         "[FailureReason](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-FailureReason)": "string",
         "[LanguageCode](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-LanguageCode)": "string",
         "[MedicalTranscriptionJobName](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-MedicalTranscriptionJobName)": "string",
         "[OutputLocationType](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-OutputLocationType)": "string",
         "[Specialty](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-Specialty)": "string",
         "[StartTime](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-StartTime)": number,
         "[TranscriptionJobStatus](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-TranscriptionJobStatus)": "string",
         "[Type](API_MedicalTranscriptionJobSummary.md#transcribe-Type-MedicalTranscriptionJobSummary-Type)": "string"
      }
   ],
   "[NextToken](#transcribe-ListMedicalTranscriptionJobs-response-NextToken)": "string",
   "[Status](#transcribe-ListMedicalTranscriptionJobs-response-Status)": "string"
}
```

## Response Elements<a name="API_ListMedicalTranscriptionJobs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [MedicalTranscriptionJobSummaries](#API_ListMedicalTranscriptionJobs_ResponseSyntax) **   <a name="transcribe-ListMedicalTranscriptionJobs-response-MedicalTranscriptionJobSummaries"></a>
A list of objects containing summary information for a transcription job\.  
Type: Array of [MedicalTranscriptionJobSummary](API_MedicalTranscriptionJobSummary.md) objects

 ** [NextToken](#API_ListMedicalTranscriptionJobs_ResponseSyntax) **   <a name="transcribe-ListMedicalTranscriptionJobs-response-NextToken"></a>
The `ListMedicalTranscriptionJobs` operation returns a page of jobs at a time\. The maximum size of the page is set by the `MaxResults` parameter\. If the number of jobs exceeds what can fit on a page, Amazon Transcribe Medical returns the `NextPage` token\. Include the token in the next request to the `ListMedicalTranscriptionJobs` operation to return in the next page of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

 ** [Status](#API_ListMedicalTranscriptionJobs_ResponseSyntax) **   <a name="transcribe-ListMedicalTranscriptionJobs-response-Status"></a>
The requested status of the medical transcription jobs returned\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED` 

## Errors<a name="API_ListMedicalTranscriptionJobs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the transcription you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_ListMedicalTranscriptionJobs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListMedicalTranscriptionJobs) 