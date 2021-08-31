# SentimentFilter<a name="API_SentimentFilter"></a>

An object that enables you to specify a particular customer or agent sentiment\. If at least 50 percent of the conversation turns \(the back\-and\-forth between two speakers\) in a specified time period match the specified sentiment, Amazon Transcribe will consider the sentiment a match\.

## Contents<a name="API_SentimentFilter_Contents"></a>

 ** AbsoluteTimeRange **   <a name="transcribe-Type-SentimentFilter-AbsoluteTimeRange"></a>
The time range, measured in seconds, of the sentiment\.  
Type: [ AbsoluteTimeRange ](API_AbsoluteTimeRange.md) object  
Required: No

 ** Negate **   <a name="transcribe-Type-SentimentFilter-Negate"></a>
Set to `TRUE` to look for sentiments that weren't specified in the request\.   
Type: Boolean  
Required: No

 ** ParticipantRole **   <a name="transcribe-Type-SentimentFilter-ParticipantRole"></a>
A value that determines whether the sentiment belongs to the customer or the agent\.  
Type: String  
Valid Values:` AGENT | CUSTOMER`   
Required: No

 ** RelativeTimeRange **   <a name="transcribe-Type-SentimentFilter-RelativeTimeRange"></a>
The time range, set in percentages, that correspond to proportion of the call\.  
Type: [ RelativeTimeRange ](API_RelativeTimeRange.md) object  
Required: No

 ** Sentiments **   <a name="transcribe-Type-SentimentFilter-Sentiments"></a>
An array that enables you to specify sentiments for the customer or agent\. You can specify one or more values\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Valid Values:` POSITIVE | NEGATIVE | NEUTRAL | MIXED`   
Required: Yes

## See Also<a name="API_SentimentFilter_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/SentimentFilter) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/SentimentFilter) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/SentimentFilter) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/SentimentFilter) 