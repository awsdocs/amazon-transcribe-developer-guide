# Creating categories<a name="call-analytics-create-categories"></a>

Call Analytics supports the creation of custom categories so you can tailor your transcript analysis to your specific business needs\.

You can create as many categories as you'd like to cover a range of different scenarios\. For each category you create, you must create between 1 and 20 rules\. Each rule is based on one of four criteria: interruptions, keywords, non\-talk time, or sentiment\. For more details on using these criteria with the [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) operation, refer to the [Rule criteria](#call-analytics-create-categories-rules) section\.

Here are a few examples of what you can do with custom categories:
+ Isolate calls with specific characteristics, such as calls that end with a negative customer sentiment
+ Identify trends in customer issues by flagging and tracking specific sets of keywords
+ Monitor compliance, such as an agent speaking a specific phrase during the first few seconds of a call
+ Gain insight into customer experience by flagging calls with many agent interruptions and negative customer sentiment
+ Compare multiple categories to measure correlations, such as analyzing whether an agent using a welcome phrase correlates with positive customer sentiment

If you run a Call Analytics job and the call characteristics match the rules you've specified in a category, Amazon Transcribe labels your job with that category\. See [call categorization output](call-analytics-output.md#call-analytics-output-categorization) for an example of a category match in JSON output\.

To create a category, you can use the **AWS Management Console**, **AWS CLI**, or **AWS SDK**; see the following for examples:

## AWS Management Console<a name="analytics-category-console"></a>

1. In the navigation pane, under Amazon Transcribe, choose **Amazon Transcribe Call Analytics**\.

1. Choose **Call analytics categories**, which takes you to the **Call analytics categories** page\. Click the **Create category** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories.png)

1. You're now on the **Create category page**\. Enter a name for your category, then choose if you're going to use a template to create a category or make one from scratch\.

   If using a template: select **Use a template \(recommended\)**, choose the template you want, then select **Create category**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-settings.png)

1. If creating a custom category: select **Create from scratch**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-custom.png)

1. Add rules to your category using the drop\-down menu\. You can add up to 20 rules per category\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-custom-rules1.png)

1. Here's an example of a category with two rules: an agent who interrupts a customer for more than 15 seconds during the call and there is negative sentiment by either the customer or the agent in the last two minutes of the call\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-custom-rules2.png)

1. When you're finished adding rules to your category, choose **Create category**\.

## AWS SDK for Python \(Boto3\)<a name="analytics-category-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to create a category using the `CategoryName` and `Rules` arguments for the [create\_call\_analytics\_category](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_call_analytics_category) method\. For more information, see [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html), [CategoryProperties](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CategoryProperties.html), and [Rule](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Rule.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
category_name = "example-call-analytics-category"
transcribe.create_call_analytics_category(
    CategoryName=category_name,
    Rules=[
        {
            'SentimentFilter': {
                'Sentiments': [
                       'NEGATIVE'
                ]
                'ParticipantRole': 'AGENT',
            }
        }
    ]
)

result = transcribe.get_call_analytics_category(CategoryName=category_name)    
print(result)
```

This example creates a category that filters for a negative agent sentiment\.

## AWS CLI<a name="analytics-category-cli"></a>

This example uses the [create\-call\-analytics\-category](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-call-analytics-category.html) command\. For more information, see [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html), [CategoryProperties](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CategoryProperties.html), and [Rule](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Rule.html)\.

This example creates a category that filters for a negative agent sentiment:

```
aws transcribe create-call-analytics-category \
--category-name my-new-category \
--rules "SentimentFilter={ParticipantRole=AGENT,Sentiments=["NEGATIVE"]}"
```

Here's another example using the [create\-call\-analytics\-category](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-call-analytics-category.html) command, and a request body that adds several rules to your category\.

```
aws transcribe create-call-analytics-category \
--cli-input-json file://filepath/my-first-analytics-category.json
```

The file *my\-first\-analytics\-category\.json* contains the following request body\.

```
{
  "CategoryName": "my-new-category",
    "Rules": [
        {
            "InterruptionFilter": {
                "AbsoluteTimeRange": {
                    "First": 60000
                },
                "Negate": true,
                "ParticipantRole": "CUSTOMER",
                "Threshold": 10000
            }
        },
        {
            "NonTalkTimeFilter": {
                "Negate": false,
                "RelativeTimeRange": {
                    "EndPercentage": 80,
                    "StartPercentage": 10
                },
                "Threshold": 20000
            }
        },
        {
            "SentimentFilter": {
                "ParticipantRole": "AGENT",
                "Sentiments": [
                    "NEGATIVE",                    
                ]
            }
        },
        {
            "TranscriptFilter": {
                "AbsoluteTimeRange": {
                    "First": 10000
                },
                "Targets": [
                    "welcome",
                    "hello"
                ],
                "TranscriptFilterType": "EXACT"
            }
        }
    ]
}
```

The preceding example creates a category with the rules:
+ The customer was not interrupted in the first 60,000 milliseconds\.
+ No one was speaking between 10% into the call through 80% into the call\.
+ The agent had a negative sentiment\.
+ The words "welcome" or "hello" were used in the first 10,000 milliseconds of the call\.

## Rule criteria<a name="call-analytics-create-categories-rules"></a>

This section outlines the types of custom rules you can create using the [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) API operation\.

### Interruption match<a name="call-analytics-create-categories-interruptions"></a>

Rules using interruptions \([InterruptionFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_InterruptionFilter.html) data type\) are designed to match:
+ Instances where an agent interrupts a customer
+ Instances where a customer interrupts an agent
+ Either participant interrupting the other
+ A lack of interruptions

Here's an example of the parameters available with [InterruptionFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_InterruptionFilter.html):

```
"InterruptionFilter": { 
    "AbsoluteTimeRange": { 
       Specify the time frame, in milliseconds, when the match should occur
    },
    "RelativeTimeRange": { 
       Specify the time frame, in percentage, when the match should occur
    },
    "Negate": Specify if you want to match the presence or absence of interruptions,
    "ParticipantRole": "Specify if you want to match speech from the agent, the customer, or both",    
    "Threshold": Specify a threshold for the amount of time, in seconds, interruptions occurred during the call
},
```

Refer to [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) and [InterruptionFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_InterruptionFilter.html) for more information on these parameters and the valid values associated with each\.

### Keyword match<a name="call-analytics-create-categories-keywords"></a>

Rules using keywords \([TranscriptFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptFilter.html) data type\) are designed to match:
+ Custom words or phrases
+ Either the presence or absence of custom words or phrases
+ Speech of the agent, the customer, or both
+ Custom words or phrases that occur at a specific time frame

Here's an example of the parameters available with [TranscriptFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptFilter.html):

```
"TranscriptFilter": { 
    "AbsoluteTimeRange": { 
       Specify the time frame, in milliseconds, when the match should occur
    },
    "RelativeTimeRange": { 
       Specify the time frame, in percentage, when the match should occur
    },
    "Negate": Specify if you want to match the presence or absence of your custom keywords,
    "ParticipantRole": "Specify if you want to match speech from the agent, the customer, or both",
    "Targets": [ "The custom words and phrases you want to match" ],
    "TranscriptFilterType": "Use this parameter to specify an exact match for the specified targets"
}
```

Refer to [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) and [TranscriptFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptFilter.html) for more information on these parameters and the valid values associated with each\.

### Non\-talk time match<a name="call-analytics-create-categories-nontalktime"></a>

Rules using non\-talk time \([NonTalkTimeFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_NonTalkTimeFilter.html) data type\) are designed to match:
+ The presence of silence at specified periods throughout the call
+ The presence of speech at specified periods throughout the call

Here's an example of the parameters available with [NonTalkTimeFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_NonTalkTimeFilter.html):

```
"NonTalkTimeFilter": { 
    "AbsoluteTimeRange": { 
 Specify the time frame, in milliseconds, when the match should occur
 },
    "RelativeTimeRange": { 
 Specify the time frame, in percentage, when the match should occur
 },
    "Negate": Specify if you want to match the presence or absence of speech,      
    "Threshold": Specify a threshold for the amount of time, in seconds, silence (or speech) occurred during the call
},
```

Refer to [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) and [NonTalkTimeFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_NonTalkTimeFilter.html) for more information on these parameters and the valid values associated with each\.

### Sentiment match<a name="call-analytics-create-categories-sentiment"></a>

Rules using sentiment \([SentimentFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_SentimentFilter.html) data type\) are designed to match:
+ Custom words or phrases
+ Either the presence or absence of custom words or phrases
+ Speech of the agent, the customer, or both
+ Custom words or phrases that occur in a specified time frame

Here's an example of the parameters available with [SentimentFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_SentimentFilter.html):

```
"SentimentFilter": { 
    "AbsoluteTimeRange": { 
    Specify the time frame, in milliseconds, when the match should occur
    },
    "RelativeTimeRange": { 
    Specify the time frame, in percentage, when the match should occur
    },
    "Negate": Specify if you want to match the presence or absence of your chosen sentiment,
    "ParticipantRole": "Specify if you want to match speech from the agent, the customer, or both",    
    "Sentiments": [ "The sentiments you want to match" ]
},
```

Refer to [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) and [SentimentFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_SentimentFilter.html) for more information on these parameters and the valid values associated with each\.