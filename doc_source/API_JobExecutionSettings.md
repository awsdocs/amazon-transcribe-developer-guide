# JobExecutionSettings<a name="API_JobExecutionSettings"></a>

Provides information about when a transcription job should be executed\.

## Contents<a name="API_JobExecutionSettings_Contents"></a>

 **AllowDeferredExecution**   <a name="transcribe-Type-JobExecutionSettings-AllowDeferredExecution"></a>
Indicates whether a job should be queued by Amazon Transcribe when the concurrent execution limit is exceeded\. When the `AllowDeferredExecution` field is true, jobs are queued and executed when the number of executing jobs falls below the concurrent execution limit\. If the field is false, Amazon Transcribe returns a `LimitExceededException` exception\.  
If you specify the `AllowDeferredExecution` field, you must specify the `DataAccessRoleArn` field\.  
Type: Boolean  
Required: No

 **DataAccessRoleArn**   <a name="transcribe-Type-JobExecutionSettings-DataAccessRoleArn"></a>
The Amazon Resource Name \(ARN\) of a role that has access to the S3 bucket that contains the input files\. Amazon Transcribe assumes this role to read queued media files\. If you have specified an output S3 bucket for the transcription results, this role should have access to the output bucket as well\.  
If you specify the `AllowDeferredExecution` field, you must specify the `DataAccessRoleArn` field\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso-{0,1}[a-z]{0,1}):iam::[0-9]{0,63}:role/[A-Za-z0-9:_/+=,@.-]{0,1024}$`   
Required: No

## See Also<a name="API_JobExecutionSettings_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/JobExecutionSettings) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/JobExecutionSettings) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/JobExecutionSettings) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/JobExecutionSettings) 