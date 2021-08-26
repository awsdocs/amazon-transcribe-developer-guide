# Tag<a name="API_Tag"></a>

A key:value pair that adds metadata to a resource used by Amazon Transcribe\. For example, a tag with the key:value pair ‘Department’:’Sales’ might be added to a resource to indicate its use by your organization's sales department\.

## Contents<a name="API_Tag_Contents"></a>

 **Key**   <a name="transcribe-Type-Tag-Key"></a>
The first part of a key:value pair that forms a tag associated with a given resource\. For example, in the tag ‘Department’:’Sales’, the key is 'Department'\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Required: Yes

 **Value**   <a name="transcribe-Type-Tag-Value"></a>
The second part of a key:value pair that forms a tag associated with a given resource\. For example, in the tag ‘Department’:’Sales’, the value is 'Sales'\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 256\.  
Required: Yes

## See Also<a name="API_Tag_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/Tag) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/Tag) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/Tag) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/Tag) 