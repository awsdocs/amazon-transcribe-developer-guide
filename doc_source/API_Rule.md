# Rule<a name="API_Rule"></a>

A condition in the call between the customer and the agent that you want to filter for\.

## Contents<a name="API_Rule_Contents"></a>

 **InterruptionFilter**   <a name="transcribe-Type-Rule-InterruptionFilter"></a>
A condition for a time period when either the customer or agent was interrupting the other person\.   
Type: [InterruptionFilter](API_InterruptionFilter.md) object  
Required: No

 **NonTalkTimeFilter**   <a name="transcribe-Type-Rule-NonTalkTimeFilter"></a>
A condition for a time period when neither the customer nor the agent was talking\.  
Type: [NonTalkTimeFilter](API_NonTalkTimeFilter.md) object  
Required: No

 **SentimentFilter**   <a name="transcribe-Type-Rule-SentimentFilter"></a>
A condition that is applied to a particular customer sentiment\.  
Type: [SentimentFilter](API_SentimentFilter.md) object  
Required: No

 **TranscriptFilter**   <a name="transcribe-Type-Rule-TranscriptFilter"></a>
A condition that catches particular words or phrases based on a exact match\. For example, if you set the phrase "I want to speak to the manager", only that exact phrase will be returned\.  
Type: [TranscriptFilter](API_TranscriptFilter.md) object  
Required: No

## See Also<a name="API_Rule_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/Rule) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/Rule) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/Rule) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/Rule) 