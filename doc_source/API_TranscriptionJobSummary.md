# TranscriptionJobSummary<a name="API_TranscriptionJobSummary"></a>

Provides a summary of information about a transcription job\.

## Contents<a name="API_TranscriptionJobSummary_Contents"></a>

 **CompletionTime**   
Timestamp of the date and time that the job completed\.  
Type: Timestamp  
Required: No

 **CreationTime**   
Timestamp of the date and time that the job was created\.  
Type: Timestamp  
Required: No

 **FailureReason**   
If the `TranscriptionJobStatus` field is `FAILED`, this field contains a description of the error\.  
Type: String  
Required: No

 **LanguageCode**   
The language code for the input speech\.  
Type: String  
Valid Values:` en-US | es-US`   
Required: No

 **TranscriptionJobName**   
The name assigned to the transcription job when it was created\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 **TranscriptionJobStatus**   
The status of the transcription job\. When the status is `COMPLETED`, use the `GetTranscriptionJob` operation to get the results of the transcription\.  
Type: String  
Valid Values:` IN_PROGRESS | FAILED | COMPLETED`   
Required: No

## See Also<a name="API_TranscriptionJobSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/TranscriptionJobSummary) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/TranscriptionJobSummary) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/TranscriptionJobSummary) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/TranscriptionJobSummary) 