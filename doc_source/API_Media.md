# Media<a name="API_Media"></a>

Describes the input media file in a transcription request\.

## Contents<a name="API_Media_Contents"></a>

 **MediaFileUri**   <a name="transcribe-Type-Media-MediaFileUri"></a>
The S3 location of the input media file\. The URI must be in the same region as the API endpoint that you are calling\. The general form is:  
 ` https://s3-<aws-region>.amazonaws.com/<bucket-name>/<keyprefix>/<objectkey> `   
For example:  
 `https://s3-us-east-1.amazonaws.com/examplebucket/example.mp4`   
 `https://s3-us-east-1.amazonaws.com/examplebucket/mediadocs/example.mp4`   
For more information about S3 object names, see [Object Keys](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-keys) in the *Amazon S3 Developer Guide*\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Required: No

## See Also<a name="API_Media_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/Media) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/Media) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/Media) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/Media) 