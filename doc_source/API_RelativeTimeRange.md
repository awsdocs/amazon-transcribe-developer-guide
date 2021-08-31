# RelativeTimeRange<a name="API_RelativeTimeRange"></a>

An object that allows percentages to specify the proportion of the call where you would like to apply a filter\. For example, you can specify the first half of the call\. You can also specify the period of time between halfway through to three\-quarters of the way through the call\. Because the length of conversation can vary between calls, you can apply relative time ranges across all calls\. 

## Contents<a name="API_RelativeTimeRange_Contents"></a>

 ** EndPercentage **   <a name="transcribe-Type-RelativeTimeRange-EndPercentage"></a>
A value that indicates the percentage of the end of the time range\. To set a relative time range, you must specify a start percentage and an end percentage\. For example, if you specify the following values:  
+ StartPercentage \- 10
+ EndPercentage \- 50
This looks at the time range starting from 10% of the way into the call to 50% of the way through the call\. For a call that lasts 100,000 milliseconds, this example range would apply from the 10,000 millisecond mark to the 50,000 millisecond mark\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 ** First **   <a name="transcribe-Type-RelativeTimeRange-First"></a>
A range that takes the portion of the call up to the time in milliseconds set by the value that you've specified\. For example, if you specify `120000`, the time range is set for the first 120,000 milliseconds of the call\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 ** Last **   <a name="transcribe-Type-RelativeTimeRange-Last"></a>
A range that takes the portion of the call from the time in milliseconds set by the value that you've specified to the end of the call\. For example, if you specify `120000`, the time range is set for the last 120,000 milliseconds of the call\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 ** StartPercentage **   <a name="transcribe-Type-RelativeTimeRange-StartPercentage"></a>
A value that indicates the percentage of the beginning of the time range\. To set a relative time range, you must specify a start percentage and an end percentage\. For example, if you specify the following values:  
+ StartPercentage \- 10
+ EndPercentage \- 50
This looks at the time range starting from 10% of the way into the call to 50% of the way through the call\. For a call that lasts 100,000 milliseconds, this example range would apply from the 10,000 millisecond mark to the 50,000 millisecond mark\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

## See Also<a name="API_RelativeTimeRange_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/RelativeTimeRange) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/RelativeTimeRange) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/RelativeTimeRange) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/RelativeTimeRange) 