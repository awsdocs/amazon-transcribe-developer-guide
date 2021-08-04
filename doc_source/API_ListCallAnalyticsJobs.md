# ListCallAnalyticsJobs<a name="API_ListCallAnalyticsJobs"></a>

List call analytics jobs with a specified status or substring that matches their names\.

## Request Syntax<a name="API_ListCallAnalyticsJobs_RequestSyntax"></a>

```
{
   "JobNameContains": "string",
   "MaxResults": number,
   "NextToken": "string",
   "Status": "string"
}
```

## Request Parameters<a name="API_ListCallAnalyticsJobs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [JobNameContains](#API_ListCallAnalyticsJobs_RequestSyntax) **   <a name="transcribe-ListCallAnalyticsJobs-request-JobNameContains"></a>
When specified, the jobs returned in the list are limited to jobs whose name contains the specified string\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** [MaxResults](#API_ListCallAnalyticsJobs_RequestSyntax) **   <a name="transcribe-ListCallAnalyticsJobs-request-MaxResults"></a>
The maximum number of call analytics jobs to return in the response\. If there are fewer results in the list, this response contains only the actual results\.   
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListCallAnalyticsJobs_RequestSyntax) **   <a name="transcribe-ListCallAnalyticsJobs-request-NextToken"></a>
If you receive a truncated result in the previous request of [ListCallAnalyticsJobs](#API_ListCallAnalyticsJobs), include `NextToken` to fetch the next set of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

 ** [Status](#API_ListCallAnalyticsJobs_RequestSyntax) **   <a name="transcribe-ListCallAnalyticsJobs-request-Status"></a>
When specified, returns only call analytics jobs with the specified status\. Jobs are ordered by creation date, with the most recent jobs returned first\. If you don't specify a status, Amazon Transcribe returns all analytics jobs ordered by creation date\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED`   
Required: No

## Response Syntax<a name="API_ListCallAnalyticsJobs_ResponseSyntax"></a>

```
{
   "CallAnalyticsJobSummaries": [ 
      { 
         "CallAnalyticsJobName": "string",
         "CallAnalyticsJobStatus": "string",
         "CompletionTime": number,
         "CreationTime": number,
         "FailureReason": "string",
         "LanguageCode": "string",
         "StartTime": number
      }
   ],
   "NextToken": "string",
   "Status": "string"
}
```

## Response Elements<a name="API_ListCallAnalyticsJobs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CallAnalyticsJobSummaries](#API_ListCallAnalyticsJobs_ResponseSyntax) **   <a name="transcribe-ListCallAnalyticsJobs-response-CallAnalyticsJobSummaries"></a>
A list of objects containing summary information for a transcription job\.  
Type: Array of [CallAnalyticsJobSummary](API_CallAnalyticsJobSummary.md) objects

 ** [NextToken](#API_ListCallAnalyticsJobs_ResponseSyntax) **   <a name="transcribe-ListCallAnalyticsJobs-response-NextToken"></a>
The [ListCallAnalyticsJobs](#API_ListCallAnalyticsJobs) operation returns a page of jobs at a time\. The maximum size of the page is set by the `MaxResults` parameter\. If there are more jobs in the list than the page size, Amazon Transcribe returns the `NextPage` token\. Include the token in your next request to the [ListCallAnalyticsJobs](#API_ListCallAnalyticsJobs) operation to return next page of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

 ** [Status](#API_ListCallAnalyticsJobs_ResponseSyntax) **   <a name="transcribe-ListCallAnalyticsJobs-response-Status"></a>
When specified, returns only call analytics jobs with that status\. Jobs are ordered by creation date, with the most recent jobs returned first\. If you don't specify a status, Amazon Transcribe returns all transcription jobs ordered by creation date\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED` 

## Errors<a name="API_ListCallAnalyticsJobs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_ListCallAnalyticsJobs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListCallAnalyticsJobs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListCallAnalyticsJobs) 