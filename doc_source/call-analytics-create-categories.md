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

## AWS Management Console<a name="analytics-category-console-batch"></a>

1. In the navigation pane, under Amazon Transcribe, choose **Amazon Transcribe Call Analytics**\.

1. Choose **Call analytics categories**, which takes you to the **Call analytics categories** page\. Select **Create category**\.  
![\[You can create a new category from the Call Analytics categories page in the Amazon Transcribe console.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories.png)

1. You're now on the **Create category page**\. Enter a name for your category, then choose if you're going to use a template to create a category or make one from scratch\.

   If using a template: select **Use a template \(recommended\)**, choose the template you want, then select **Create category**\.  
![\[Specify whether you want your category used for batch or real-time (streaming) transcriptions.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-settings.png)

1. If creating a custom category: select **Create from scratch**\.  
![\[You can either use a template for your new category or create it from scratch.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-custom.png)

1. Add rules to your category using the drop\-down menu\. You can add up to 20 rules per category\.  
![\[If you create a category from scratch, you must specify at least one rule.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-custom-rules1.png)

1. Here's an example of a category with two rules: an agent who interrupts a customer for more than 15 seconds during the call and there is negative sentiment by either the customer or the agent in the last two minutes of the call\.  
![\[Select a rule type from the drop-down menu.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-custom-rules2.png)

1. When you're finished adding rules to your category, choose **Create category**\.

## AWS CLI<a name="analytics-category-cli"></a>

This example uses the [create\-call\-analytics\-category](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-call-analytics-category.html) command\. For more information, see [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html), [CategoryProperties](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CategoryProperties.html), and [Rule](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Rule.html)\.

The following example creates a category with the rules:
+ The customer was interrupted in the first 60,000 milliseconds\. The duration of these interruptions lasted at least 10,000 milliseconds\.
+ There was a period of silence that lasted at least 20,000 milliseconds between 10% into the call and 80% into the call\.
+ The agent had a negative sentiment at some point in the call\.
+ The words "welcome" or "hello" were not used in the first 10,000 milliseconds of the call\.

This example uses the [create\-call\-analytics\-category](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-call-analytics-category.html) command, and a request body that adds several rules to your category\.

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
                "Negate": false,
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
                    "NEGATIVE"                    
                ]
            }
        },
        {
            "TranscriptFilter": {
                "Negate": true,
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

## AWS SDK for Python \(Boto3\)<a name="analytics-category-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to create a category using the `CategoryName` and `Rules` arguments for the [create\_call\_analytics\_category](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_call_analytics_category) method\. For more information, see [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html), [CategoryProperties](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CategoryProperties.html), and [Rule](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Rule.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe using AWS SDKs](service_code_examples.md) chapter\.

The following example creates a category with the rules:
+ The customer was interrupted in the first 60,000 milliseconds\. The duration of these interruptions lasted at least 10,000 milliseconds\.
+ There was a period of silence that lasted at least 20,000 milliseconds between 10% into the call and 80% into the call\.
+ The agent had a negative sentiment at some point in the call\.
+ The words "welcome" or "hello" were not used in the first 10,000 milliseconds of the call\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
category_name = "my-new-category"
transcribe.create_call_analytics_category(
    CategoryName = category_name,
    Rules = [
        {
            'InterruptionFilter': {
                'AbsoluteTimeRange': {
                    'First': 60000
                },
                'Negate': False,
                'ParticipantRole': 'CUSTOMER',
                'Threshold': 10000
            }
        },
        {
            'NonTalkTimeFilter': {
                'Negate': False,
                'RelativeTimeRange': {
                    'EndPercentage': 80,
                    'StartPercentage': 10
                },
                'Threshold': 20000
            }
        },
        {
            'SentimentFilter': {
                'ParticipantRole': 'AGENT',
                'Sentiments': [
                    'NEGATIVE'                    
                ]
            }
        },
        {
            'TranscriptFilter': {
                'Negate': True,
                'AbsoluteTimeRange': {
                    'First': 10000
                },
                'Targets': [
                    'welcome',
                    'hello'
                ],
                'TranscriptFilterType': 'EXACT'
            }
        }
    ]
    
)

result = transcribe.get_call_analytics_category(CategoryName = category_name)    
print(result)
```

## Rule criteria<a name="call-analytics-create-categories-rules"></a>

This section outlines the types of custom rules you can create using the [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) API operation\.

### Interruption match<a name="call-analytics-create-categories-interruptions"></a>

Rules using interruptions \([InterruptionFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_InterruptionFilter.html) data type\) are designed to match:
+ Instances where an agent interrupts a customer
+ Instances where a customer interrupts an agent
+ Any participant interrupting the other
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
    "ParticipantRole": Specify if you want to match speech from the agent, the customer, or both,    
    "Threshold": Specify a threshold for the amount of time, in seconds, interruptions occurred during the call
},
```

Refer to [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) and [InterruptionFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_InterruptionFilter.html) for more information on these parameters and the valid values associated with each\.

### Keyword match<a name="call-analytics-create-categories-keywords"></a>

Rules using keywords \([TranscriptFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptFilter.html) data type\) are designed to match:
+ Custom words or phrases spoken by the agent, the customer, or both
+ Custom words or phrases **not** spoken by the agent, the customer, or both
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
    "ParticipantRole": Specify if you want to match speech from the agent, the customer, or both,
    "Targets": [ The custom words and phrases you want to match ],
    "TranscriptFilterType": Use this parameter to specify an exact match for the specified targets
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
+ The presence or absence of a positive sentiment felt by the customer, agent, or both at specified points in the call
+ The presence or absence of a negative sentiment felt by the customer, agent, or both at specified points in the call
+ The presence or absence of a neutral sentiment felt by the customer, agent, or both at specified points in the call
+ The presence or absence of a mixed sentiment felt by the customer, agent, or both at specified points in the call

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
    "ParticipantRole": Specify if you want to match speech from the agent, the customer, or both,    
    "Sentiments": [ The sentiments you want to match ]
},
```

Refer to [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) and [SentimentFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_SentimentFilter.html) for more information on these parameters and the valid values associated with each\.