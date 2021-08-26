# ChannelDefinition<a name="API_ChannelDefinition"></a>

For a call analytics job, an object that indicates the audio channel that belongs to the agent and the audio channel that belongs to the customer\.

## Contents<a name="API_ChannelDefinition_Contents"></a>

 **ChannelId**   <a name="transcribe-Type-ChannelDefinition-ChannelId"></a>
A value that indicates the audio channel\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 1\.  
Required: No

 **ParticipantRole**   <a name="transcribe-Type-ChannelDefinition-ParticipantRole"></a>
Indicates whether the person speaking on the audio channel is the agent or customer\.  
Type: String  
Valid Values:` AGENT | CUSTOMER`   
Required: No

## See Also<a name="API_ChannelDefinition_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ChannelDefinition) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ChannelDefinition) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/ChannelDefinition) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ChannelDefinition) 