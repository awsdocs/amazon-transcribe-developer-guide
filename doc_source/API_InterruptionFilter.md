# InterruptionFilter<a name="API_InterruptionFilter"></a>

An object that enables you to configure your category to be applied to call analytics jobs where either the customer or agent was interrupted\.

## Contents<a name="API_InterruptionFilter_Contents"></a>

 ** AbsoluteTimeRange **   <a name="transcribe-Type-InterruptionFilter-AbsoluteTimeRange"></a>
An object you can use to specify a time range \(in milliseconds\) for when you'd want to find the interruption\. For example, you could search for an interruption between the 30,000 millisecond mark and the 45,000 millisecond mark\. You could also specify the time period as the first 15,000 milliseconds or the last 15,000 milliseconds\.   
Type: [ AbsoluteTimeRange ](API_AbsoluteTimeRange.md) object  
Required: No

 ** Negate **   <a name="transcribe-Type-InterruptionFilter-Negate"></a>
Set to `TRUE` to look for a time period where there was no interruption\.  
Type: Boolean  
Required: No

 ** ParticipantRole **   <a name="transcribe-Type-InterruptionFilter-ParticipantRole"></a>
Indicates whether the caller or customer was interrupting\.  
Type: String  
Valid Values:` AGENT | CUSTOMER`   
Required: No

 ** RelativeTimeRange **   <a name="transcribe-Type-InterruptionFilter-RelativeTimeRange"></a>
An object that allows percentages to specify the proportion of the call where there was a interruption\. For example, you can specify the first half of the call\. You can also specify the period of time between halfway through to three\-quarters of the way through the call\. Because the length of conversation can vary between calls, you can apply relative time ranges across all calls\.  
Type: [ RelativeTimeRange ](API_RelativeTimeRange.md) object  
Required: No

 ** Threshold **   <a name="transcribe-Type-InterruptionFilter-Threshold"></a>
The duration of the interruption\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 14400000\.  
Required: No

## See Also<a name="API_InterruptionFilter_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/InterruptionFilter) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/InterruptionFilter) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/InterruptionFilter) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/InterruptionFilter) 