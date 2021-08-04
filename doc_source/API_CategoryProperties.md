# CategoryProperties<a name="API_CategoryProperties"></a>

An object that contains the rules and additional information about a call analytics category\.

## Contents<a name="API_CategoryProperties_Contents"></a>

 **CategoryName**   <a name="transcribe-Type-CategoryProperties-CategoryName"></a>
The name of the call analytics category\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 **CreateTime**   <a name="transcribe-Type-CategoryProperties-CreateTime"></a>
A timestamp that shows when the call analytics category was created\.  
Type: Timestamp  
Required: No

 **LastUpdateTime**   <a name="transcribe-Type-CategoryProperties-LastUpdateTime"></a>
A timestamp that shows when the call analytics category was most recently updated\.  
Type: Timestamp  
Required: No

 **Rules**   <a name="transcribe-Type-CategoryProperties-Rules"></a>
The rules used to create a call analytics category\.  
Type: Array of [Rule](API_Rule.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 20 items\.  
Required: No

## See Also<a name="API_CategoryProperties_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/CategoryProperties) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/CategoryProperties) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/CategoryProperties) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/CategoryProperties) 