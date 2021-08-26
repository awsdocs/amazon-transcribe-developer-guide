# AbsoluteTimeRange<a name="API_AbsoluteTimeRange"></a>

A time range, set in seconds, between two points in the call\.

## Contents<a name="API_AbsoluteTimeRange_Contents"></a>

 **EndTime**   <a name="transcribe-Type-AbsoluteTimeRange-EndTime"></a>
A value that indicates the end of the time range in milliseconds\. To set absolute time range, you must specify a start time and an end time\. For example, if you specify the following values:  
+ StartTime \- 10000
+ Endtime \- 50000
The time range is set between 10,000 milliseconds and 50,000 milliseconds into the call\.   
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 14400000\.  
Required: No

 **First**   <a name="transcribe-Type-AbsoluteTimeRange-First"></a>
A time range from the beginning of the call to the value that you've specified\. For example, if you specify 100000, the time range is set to the first 100,000 milliseconds of the call\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 14400000\.  
Required: No

 **Last**   <a name="transcribe-Type-AbsoluteTimeRange-Last"></a>
A time range from the value that you've specified to the end of the call\. For example, if you specify 100000, the time range is set to the last 100,000 milliseconds of the call\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 14400000\.  
Required: No

 **StartTime**   <a name="transcribe-Type-AbsoluteTimeRange-StartTime"></a>
A value that indicates the beginning of the time range in seconds\. To set absolute time range, you must specify a start time and an end time\. For example, if you specify the following values:  
+ StartTime \- 10000
+ Endtime \- 50000
The time range is set between 10,000 milliseconds and 50,000 milliseconds into the call\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 14400000\.  
Required: No

## See Also<a name="API_AbsoluteTimeRange_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/AbsoluteTimeRange) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/AbsoluteTimeRange) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/AbsoluteTimeRange) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/AbsoluteTimeRange) 