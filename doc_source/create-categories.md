# Using categories and rules<a name="create-categories"></a>

You can use call analytics categories to flag particular conversational characteristics in your call analytics job\. For each category you create, you must create between 1 and 20 rules\. Each rule contains one *filter* to identify criteria applicable to a category\. You can create filters for the following:
+ Non\-talk time: When neither the customer nor the agent is talking\.
+ Interruptions: When either the customer or the agent is interrupting the other person\.
+ Customer or agent sentiment: How either the customer or the agent is feeling during a specified time period\. If at least 50 percent of the conversation turns \(the back\-and\-forth between two speakers\) in a specified time period match the specified sentiment, Amazon Transcribe will consider the sentiment a match\.
+ Call categorization: Matches part of the transcription based on an exact phrase\. For example, if you filter for the customer saying "I want to speak to the manager", Amazon Transcribe filters for that exact phrase\.

To create a category, you can use the **Amazon Transcribe Console**, **AWS CLI**, or **AWS SDK**; see below for instructions:

## Console<a name="analytics-category-console"></a>

1. In the navigation pane, under Amazon Transcribe, choose **Amazon Transcribe Call Analytics**\.

1. Choose **Call analytics categories**, which takes you to the **Call analytics categories** page\. Click the **Create category** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories.png)

1. You're now on the **Create category page**\. Enter a name for the category, then choose whether you're going to use a template to create a category\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-categories-settings.png)

1. Choose **Create category**\.

## AWS SDK for Python \(Boto3\)<a name="analytics-category-sdk"></a>

The following example uses the AWS SDK for Python \(Boto3\) to create a category by using the `CategoryName` and `Rules` arguments for the [create\_call\_analytics\_category](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_call_analytics_category) method:

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
category_name = "example-call-analytics-category"
transcribe.create_call_analytics_category(
    CategoryName=category_name,
    Rules=[{'SentimentFilter': {'ParticipantRole': 'AGENT', 
                    'Sentiments': ['NEGATIVE']}}]
)
result = transcribe.get_call_analytics_category(CategoryName=category_name)    
print(result)
```

This example creates a category that filters for a negative agent sentiment\.

## AWS CLI<a name="analytics-category-cli"></a>

This example uses the [create\-call\-analytics\-category](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-call-analytics-category.html) command\.

This example creates a category that filters for a negative agent sentiment:

```
aws transcribe create-call-analytics-category \
--category-name your-category-name \
--rules "SentimentFilter={ParticipantRole=AGENT,Sentiments=["NEGATIVE"]}"
```

Here's another example using the [create\-call\-analytics\-category](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-call-analytics-category.html) command, and a request body that adds several rules to your category\.

```
aws transcribe create-call-analytics-category \
--cli-input-json file://filepath/example-start-command.json
```

The file *example\-start\-command\.json* contains the following request body\.

```
{
  "CategoryName": "example-call-analytics-category",
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

The above example creates a category with the rules:
+ The customer was not interrupted in the first 60,000 milliseconds\.
+ No one was speaking between 10% into the call through 80% into the call\.
+ The agent had a negative sentiment\.
+ The words "welcome" or "hello" were used in the first 10,000 milliseconds of the call\.