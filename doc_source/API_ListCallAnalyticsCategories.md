# ListCallAnalyticsCategories<a name="API_ListCallAnalyticsCategories"></a>

Provides more information about the call analytics categories that you've created\. You can use the information in this list to find a specific category\. You can then use the [GetCallAnalyticsCategory](API_GetCallAnalyticsCategory.md) operation to get more information about it\.

## Request Syntax<a name="API_ListCallAnalyticsCategories_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListCallAnalyticsCategories_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListCallAnalyticsCategories_RequestSyntax) **   <a name="transcribe-ListCallAnalyticsCategories-request-MaxResults"></a>
The maximum number of categories to return in each page of results\. If there are fewer results than the value you specify, only the actual results are returned\. If you do not specify a value, the default of 5 is used\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListCallAnalyticsCategories_RequestSyntax) **   <a name="transcribe-ListCallAnalyticsCategories-request-NextToken"></a>
When included, `NextToken`fetches the next set of categories if the result of the previous request was truncated\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

## Response Syntax<a name="API_ListCallAnalyticsCategories_ResponseSyntax"></a>

```
{
   "Categories": [ 
      { 
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
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListCallAnalyticsCategories_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Categories](#API_ListCallAnalyticsCategories_ResponseSyntax) **   <a name="transcribe-ListCallAnalyticsCategories-response-Categories"></a>
A list of objects containing information about analytics categories\.  
Type: Array of [CategoryProperties](API_CategoryProperties.md) objects

 ** [NextToken](#API_ListCallAnalyticsCategories_ResponseSyntax) **   <a name="transcribe-ListCallAnalyticsCategories-response-NextToken"></a>
The [ListCallAnalyticsCategories](#API_ListCallAnalyticsCategories) operation returns a page of jobs at a time\. The maximum size of the list is set by the `MaxResults` parameter\. If there are more categories in the list than the page size, Amazon Transcribe returns the `NextPage` token\. Include the token in the next request to the [ListCallAnalyticsCategories](#API_ListCallAnalyticsCategories) operation to return the next page of analytics categories\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

## Errors<a name="API_ListCallAnalyticsCategories_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_ListCallAnalyticsCategories_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListCallAnalyticsCategories) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListCallAnalyticsCategories) 