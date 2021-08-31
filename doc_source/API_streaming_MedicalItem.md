# MedicalItem<a name="API_streaming_MedicalItem"></a>

A word, phrase, or punctuation mark that is transcribed from the input audio\.

## Contents<a name="API_streaming_MedicalItem_Contents"></a>

 ** Confidence **   <a name="transcribe-Type-streaming_MedicalItem-Confidence"></a>
A value between 0 and 1 for an item that is a confidence score that Amazon Transcribe Medical assigns to each word that it transcribes\.  
Type: Double  
Required: No

 ** Content **   <a name="transcribe-Type-streaming_MedicalItem-Content"></a>
The word or punctuation mark that was recognized in the input audio\.  
Type: String  
Required: No

 ** EndTime **   <a name="transcribe-Type-streaming_MedicalItem-EndTime"></a>
The number of seconds into an audio stream that indicates the creation time of an item\.  
Type: Double  
Required: No

 ** Speaker **   <a name="transcribe-Type-streaming_MedicalItem-Speaker"></a>
If speaker identification is enabled, shows the integer values that correspond to the different speakers identified in the stream\. For example, if the value of `Speaker` in the stream is either a `0` or a `1`, that indicates that Amazon Transcribe Medical has identified two speakers in the stream\. The value of `0` corresponds to one speaker and the value of `1` corresponds to the other speaker\.  
Type: String  
Required: No

 ** StartTime **   <a name="transcribe-Type-streaming_MedicalItem-StartTime"></a>
The number of seconds into an audio stream that indicates the creation time of an item\.  
Type: Double  
Required: No

 ** Type **   <a name="transcribe-Type-streaming_MedicalItem-Type"></a>
The type of the item\. `PRONUNCIATION` indicates that the item is a word that was recognized in the input audio\. `PUNCTUATION` indicates that the item was interpreted as a pause in the input audio, such as a period to indicate the end of a sentence\.  
Type: String  
Valid Values:` pronunciation | punctuation`   
Required: No

## See Also<a name="API_streaming_MedicalItem_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/MedicalItem) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/MedicalItem) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/MedicalItem) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/MedicalItem) 