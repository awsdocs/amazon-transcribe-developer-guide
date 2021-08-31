# Transcript<a name="API_Transcript"></a>

Identifies the location of a transcription\.

## Contents<a name="API_Transcript_Contents"></a>

 ** RedactedTranscriptFileUri **   <a name="transcribe-Type-Transcript-RedactedTranscriptFileUri"></a>
The S3 object location of the redacted transcript\.  
Use this URI to access the redacted transcript\. If you specified an S3 bucket in the `OutputBucketName` field when you created the job, this is the URI of that bucket\. If you chose to store the transcript in Amazon Transcribe, this is a shareable URL that provides secure access to that location\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

 ** TranscriptFileUri **   <a name="transcribe-Type-Transcript-TranscriptFileUri"></a>
The S3 object location of the transcript\.  
Use this URI to access the transcript\. If you specified an S3 bucket in the `OutputBucketName` field when you created the job, this is the URI of that bucket\. If you chose to store the transcript in Amazon Transcribe, this is a shareable URL that provides secure access to that location\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

## See Also<a name="API_Transcript_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/Transcript) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/Transcript) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/Transcript) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/Transcript) 