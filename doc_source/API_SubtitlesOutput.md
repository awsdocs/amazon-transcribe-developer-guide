# SubtitlesOutput<a name="API_SubtitlesOutput"></a>

Specify the output format for your subtitle file\.

## Contents<a name="API_SubtitlesOutput_Contents"></a>

 ** Formats **   <a name="transcribe-Type-SubtitlesOutput-Formats"></a>
Specify the output format for your subtitle file; if you select both SRT and VTT formats, two output files are genereated\.  
Type: Array of strings  
Valid Values:` vtt | srt`   
Required: No

 ** SubtitleFileUris **   <a name="transcribe-Type-SubtitlesOutput-SubtitleFileUris"></a>
Choose the output location for your subtitle file\. This location must be an S3 bucket\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

## See Also<a name="API_SubtitlesOutput_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/SubtitlesOutput) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/SubtitlesOutput) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/SubtitlesOutput) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/SubtitlesOutput) 