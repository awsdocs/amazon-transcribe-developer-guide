# TranscriptFilter<a name="API_TranscriptFilter"></a>

Matches the output of the transcription to either the specific phrases that you specify, or the intent of the phrases that you specify\.

## Contents<a name="API_TranscriptFilter_Contents"></a>

 ** AbsoluteTimeRange **   <a name="transcribe-Type-TranscriptFilter-AbsoluteTimeRange"></a>
A time range, set in seconds, between two points in the call\.  
Type: [ AbsoluteTimeRange ](API_AbsoluteTimeRange.md) object  
Required: No

 ** Negate **   <a name="transcribe-Type-TranscriptFilter-Negate"></a>
If `TRUE`, the rule that you specify is applied to everything except for the phrases that you specify\.  
Type: Boolean  
Required: No

 ** ParticipantRole **   <a name="transcribe-Type-TranscriptFilter-ParticipantRole"></a>
Determines whether the customer or the agent is speaking the phrases that you've specified\.  
Type: String  
Valid Values:` AGENT | CUSTOMER`   
Required: No

 ** RelativeTimeRange **   <a name="transcribe-Type-TranscriptFilter-RelativeTimeRange"></a>
An object that allows percentages to specify the proportion of the call where you would like to apply a filter\. For example, you can specify the first half of the call\. You can also specify the period of time between halfway through to three\-quarters of the way through the call\. Because the length of conversation can vary between calls, you can apply relative time ranges across all calls\.  
Type: [ RelativeTimeRange ](API_RelativeTimeRange.md) object  
Required: No

 ** Targets **   <a name="transcribe-Type-TranscriptFilter-Targets"></a>
The phrases that you're specifying for the transcript filter to match\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `.*\S.*`   
Required: Yes

 ** TranscriptFilterType **   <a name="transcribe-Type-TranscriptFilter-TranscriptFilterType"></a>
Matches the phrase to the transcription output in a word for word fashion\. For example, if you specify the phrase "I want to speak to the manager\." Amazon Transcribe attempts to match that specific phrase to the transcription\.  
Type: String  
Valid Values:` EXACT`   
Required: Yes

## See Also<a name="API_TranscriptFilter_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/TranscriptFilter) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/TranscriptFilter) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/TranscriptFilter) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/TranscriptFilter) 