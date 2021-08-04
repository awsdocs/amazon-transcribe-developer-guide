# Item<a name="API_streaming_Item"></a>

A word, phrase, or punctuation mark that is transcribed from the input audio\.

## Contents<a name="API_streaming_Item_Contents"></a>

 **Confidence**   <a name="transcribe-Type-streaming_Item-Confidence"></a>
A value between 0 and 1 for an item that is a confidence score that Amazon Transcribe assigns to each word or phrase that it transcribes\.  
Type: Double  
Required: No

 **Content**   <a name="transcribe-Type-streaming_Item-Content"></a>
The word or punctuation that was recognized in the input audio\.  
Type: String  
Required: No

 **EndTime**   <a name="transcribe-Type-streaming_Item-EndTime"></a>
The offset from the beginning of the audio stream to the end of the audio that resulted in the item\.  
Type: Double  
Required: No

 **Speaker**   <a name="transcribe-Type-streaming_Item-Speaker"></a>
If speaker identification is enabled, shows the speakers identified in the real\-time stream\.  
Type: String  
Required: No

 **Stable**   <a name="transcribe-Type-streaming_Item-Stable"></a>
If partial result stabilization has been enabled, indicates whether the word or phrase in the item is stable\. If `Stable` is `true`, the result is stable\.  
Type: Boolean  
Required: No

 **StartTime**   <a name="transcribe-Type-streaming_Item-StartTime"></a>
The offset from the beginning of the audio stream to the beginning of the audio that resulted in the item\.  
Type: Double  
Required: No

 **Type**   <a name="transcribe-Type-streaming_Item-Type"></a>
The type of the item\. `PRONUNCIATION` indicates that the item is a word that was recognized in the input audio\. `PUNCTUATION` indicates that the item was interpreted as a pause in the input audio\.  
Type: String  
Valid Values:` pronunciation | punctuation`   
Required: No

 **VocabularyFilterMatch**   <a name="transcribe-Type-streaming_Item-VocabularyFilterMatch"></a>
Indicates whether a word in the item matches a word in the vocabulary filter you've chosen for your real\-time stream\. If `true` then a word in the item matches your vocabulary filter\.  
Type: Boolean  
Required: No

## See Also<a name="API_streaming_Item_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/Item) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/Item) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/Item) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/Item) 