# ListTranscriptionJobs<a name="API_ListTranscriptionJobs"></a>

Lists transcription jobs with the specified status\.

## Request Syntax<a name="API_ListTranscriptionJobs_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "Status": "string"
}
```

## Request Parameters<a name="API_ListTranscriptionJobs_RequestParameters"></a>

For information about the parameters that are common to all actions, see Common Parameters\.

The request accepts the following data in JSON format\.

 ** MaxResults **   
The maximum number of jobs to return in the response\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** NextToken **   
If the result of the previous request to `ListTranscriptionJobs` was truncated, include the `NextToken` to fetch the next set of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Required: No

 ** Status **   
When specified, returns only transcription jobs with the specified status\.  
Type: String  
Valid Values:` IN_PROGRESS | FAILED | COMPLETED`   
Required: Yes

## Response Syntax<a name="API_ListTranscriptionJobs_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "Status": "string",
   "TranscriptionJobSummaries": [ 
      { 
         "CompletionTime": number,
         "CreationTime": number,
         "FailureReason": "string",
         "LanguageCode": "string",
         "TranscriptionJobName": "string",
         "TranscriptionJobStatus": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListTranscriptionJobs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** NextToken **   
The `ListTranscriptionJobs` operation returns a page of jobs at a time\. The size of the page is set by the `MaxResults` parameter\. If there are more jobs in the list than the page size, Amazon Transcribe returns the `NextPage` token\. Include the token in the next request to the `ListTranscriptionJobs` operation to return in the next page of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.

 ** Status **   
The requested status of the jobs returned\.  
Type: String  
Valid Values:` IN_PROGRESS | FAILED | COMPLETED` 

 ** TranscriptionJobSummaries **   
A list of objects containing summary information for a transcription job\.  
Type: Array of [TranscriptionJobSummary](API_TranscriptionJobSummary.md) objects

## Errors<a name="API_ListTranscriptionJobs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
There is a problem with one of the input fields\. Check the S3 bucket name, make sure that the job name is not a duplicate, and confirm that you are using the correct file format\. Then resend your request\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 400

 **LimitExceededException**   
Either you have sent too many requests or your input file is longer than 2 hours\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_ListTranscriptionJobs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListTranscriptionJobs) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/ListTranscriptionJobs) 