# AudioEvent<a name="API_streaming_AudioEvent"></a>

Provides a wrapper for the audio chunks that you are sending\.

For information on audio encoding in Amazon Transcribe, see [Speech input](https://docs.aws.amazon.com/transcribe/latest/dg/input.html)\. For information on audio encoding formats in Amazon Transcribe Medical, see [Speech input](https://docs.aws.amazon.com/transcribe/latest/dg/input-med.html)\.

## Contents<a name="API_streaming_AudioEvent_Contents"></a>

 **AudioChunk**   <a name="transcribe-Type-streaming_AudioEvent-AudioChunk"></a>
An audio blob that contains the next part of the audio that you want to transcribe\. The maximum audio chunk size is 32 KB\.  
Type: Base64\-encoded binary data object  
Required: No

## See Also<a name="API_streaming_AudioEvent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/AudioEvent) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/AudioEvent) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/AudioEvent) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/AudioEvent) 