# MedicalTranscript<a name="API_MedicalTranscript"></a>

Identifies the location of a medical transcript\.

## Contents<a name="API_MedicalTranscript_Contents"></a>

 **TranscriptFileUri**   <a name="transcribe-Type-MedicalTranscript-TranscriptFileUri"></a>
The S3 object location of the medical transcript\.  
Use this URI to access the medical transcript\. This URI points to the S3 bucket you created to store the medical transcript\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

## See Also<a name="API_MedicalTranscript_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/MedicalTranscript) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/MedicalTranscript) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/MedicalTranscript) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/MedicalTranscript) 