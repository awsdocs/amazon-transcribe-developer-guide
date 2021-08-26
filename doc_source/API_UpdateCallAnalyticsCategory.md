# UpdateCallAnalyticsCategory<a name="API_UpdateCallAnalyticsCategory"></a>

Updates the call analytics category with new values\. The `UpdateCallAnalyticsCategory` operation overwrites all of the existing information with the values that you provide in the request\. 

## Request Syntax<a name="API_UpdateCallAnalyticsCategory_RequestSyntax"></a>

```
{
   "CategoryName": "string",
   "Rules": [ 
      { 
         "InterruptionFilter": { 
            "AbsoluteTimeRange": { 
               "EndTime": number,
               "First": number,
               "Last": number,
               "StartTime": number
            },
            "Negate": boolean,
            "ParticipantRole": "string",
            "RelativeTimeRange": { 
               "EndPercentage": number,
               "First": number,
               "Last": number,
               "StartPercentage": number
            },
            "Threshold": number
         },
         "NonTalkTimeFilter": { 
            "AbsoluteTimeRange": { 
               "EndTime": number,
               "First": number,
               "Last": number,
               "StartTime": number
            },
            "Negate": boolean,
            "RelativeTimeRange": { 
               "EndPercentage": number,
               "First": number,
               "Last": number,
               "StartPercentage": number
            },
            "Threshold": number
         },
         "SentimentFilter": { 
            "AbsoluteTimeRange": { 
               "EndTime": number,
               "First": number,
               "Last": number,
               "StartTime": number
            },
            "Negate": boolean,
            "ParticipantRole": "string",
            "RelativeTimeRange": { 
               "EndPercentage": number,
               "First": number,
               "Last": number,
               "StartPercentage": number
            },
            "Sentiments": [ "string" ]
         },
         "TranscriptFilter": { 
            "AbsoluteTimeRange": { 
               "EndTime": number,
               "First": number,
               "Last": number,
               "StartTime": number
            },
            "Negate": boolean,
            "ParticipantRole": "string",
            "RelativeTimeRange": { 
               "EndPercentage": number,
               "First": number,
               "Last": number,
               "StartPercentage": number
            },
            "Targets": [ "string" ],
            "TranscriptFilterType": "string"
         }
      }
   ]
}
```

## Request Parameters<a name="API_UpdateCallAnalyticsCategory_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CategoryName](#API_UpdateCallAnalyticsCategory_RequestSyntax) **   <a name="transcribe-UpdateCallAnalyticsCategory-request-CategoryName"></a>
The name of the analytics category to update\. The name is case sensitive\. If you try to update a call analytics category with the same name as a previous category you will receive a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

 ** [Rules](#API_UpdateCallAnalyticsCategory_RequestSyntax) **   <a name="transcribe-UpdateCallAnalyticsCategory-request-Rules"></a>
The rules used for the updated analytics category\. The rules that you provide in this field replace the ones that are currently being used\.   
Type: Array of [Rule](API_Rule.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 20 items\.  
Required: Yes

## Response Syntax<a name="API_UpdateCallAnalyticsCategory_ResponseSyntax"></a>

```
{
   "CategoryProperties": { 
      "CategoryName": "string",
      "CreateTime": number,
      "LastUpdateTime": number,
      "Rules": [ 
         { 
            "InterruptionFilter": { 
               "AbsoluteTimeRange": { 
                  "EndTime": number,
                  "First": number,
                  "Last": number,
                  "StartTime": number
               },
               "Negate": boolean,
               "ParticipantRole": "string",
               "RelativeTimeRange": { 
                  "EndPercentage": number,
                  "First": number,
                  "Last": number,
                  "StartPercentage": number
               },
               "Threshold": number
            },
            "NonTalkTimeFilter": { 
               "AbsoluteTimeRange": { 
                  "EndTime": number,
                  "First": number,
                  "Last": number,
                  "StartTime": number
               },
               "Negate": boolean,
               "RelativeTimeRange": { 
                  "EndPercentage": number,
                  "First": number,
                  "Last": number,
                  "StartPercentage": number
               },
               "Threshold": number
            },
            "SentimentFilter": { 
               "AbsoluteTimeRange": { 
                  "EndTime": number,
                  "First": number,
                  "Last": number,
                  "StartTime": number
               },
               "Negate": boolean,
               "ParticipantRole": "string",
               "RelativeTimeRange": { 
                  "EndPercentage": number,
                  "First": number,
                  "Last": number,
                  "StartPercentage": number
               },
               "Sentiments": [ "string" ]
            },
            "TranscriptFilter": { 
               "AbsoluteTimeRange": { 
                  "EndTime": number,
                  "First": number,
                  "Last": number,
                  "StartTime": number
               },
               "Negate": boolean,
               "ParticipantRole": "string",
               "RelativeTimeRange": { 
                  "EndPercentage": number,
                  "First": number,
                  "Last": number,
                  "StartPercentage": number
               },
               "Targets": [ "string" ],
               "TranscriptFilterType": "string"
            }
         }
      ]
   }
}
```

## Response Elements<a name="API_UpdateCallAnalyticsCategory_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CategoryProperties](#API_UpdateCallAnalyticsCategory_ResponseSyntax) **   <a name="transcribe-UpdateCallAnalyticsCategory-response-CategoryProperties"></a>
The attributes describing the analytics category\. You can see information such as the rules that you've used to update the category and when the category was originally created\.   
Type: [CategoryProperties](API_CategoryProperties.md) object

## Errors<a name="API_UpdateCallAnalyticsCategory_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **ConflictException**   
There is already a resource with that name\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

 **NotFoundException**   
We can't find the requested resource\. Check the name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_UpdateCallAnalyticsCategory_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/UpdateCallAnalyticsCategory) 