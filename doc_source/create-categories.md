# Using categories and rules<a name="create-categories"></a>

You can use call analytics categories to flag particular conversational characteristics in your analytics job\. For each category you create, you must create between 1 and 20 rules\. Each rule contains one *filter* to identify criteria applicable to a category\. You can create filters for the following:
+ Non\-talk time: When neither the customer nor the agent is talking\.
+ Interruptions: When either the customer or the agent is interrupting the other person\.
+ Customer or agent sentiment: How either the customer or the agent is feeling during a specified time period\. If at least 50 percent of the conversation turns \(the back\-and\-forth between two speakers\) in a specified time period match the specified sentiment, Amazon Transcribe will consider the sentiment a match\.
+ Call categorization: Matches part of the transcription based on an exact phrase\. For example, if you filter for the customer saying "I want to speak to the manager", Amazon Transcribe filters for that exact phrase\.

To create a category, you can use either the Amazon Transcribe console or the API\.

## Console<a name="create-category-console"></a>

To create a category, you define one or more rules\. Each rule can have one filter\.

**To transcribe a multi\-channel audio file \(console\)**

1. Sign in to AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe, choose **Amazon Transcribe Call Analytics**\.

1. Choose **Call analytics categories**\.

1. Choose **Create category**\.

1. For **Category name**, enter a name for the category\.

1. For **Category creation method**, choose whether you're going to use a template to create a category\.

1. Specify the rules for the category\.

1. Choose **Create category**\.

## API<a name="create-category-api"></a>

**To create a category \(API\)**
+ In the [CreateCallAnalyticsCategory](API_CreateCallAnalyticsCategory.md) operation, specify the following:

  1. `CallAnalyticsCategoryName` – specify a name for the category that is unique to your AWS account\.

  1. `Rules` – specify one or more rules\. A rule could be one of the following:
     + `InterruptionFilter`
     + `NonTalkTimeFilter`
     + `SentimentFilter`
     + `TranscriptFilter`

The following is an example request using the AWS SDK for Python \(Boto3\), which creates a category that filters for the agent having a negative sentiment\.

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

## AWS CLI<a name="category-cli"></a>

**To create a call analytics category \(AWS CLI\)**
+ Run the following code\. This code creates a category with the rules:
  + The customer was not interrupted in the first 60,000 milliseconds\.
  + No one was speaking between 10% into the call through 80% into the call\.
  + The agent had a negative sentiment\.
  + The words "welcome" or "hello" were used in the first 10,000 milliseconds of the call\.

  ```
                      
  aws transcribe create-call-analytics-category \
  --cli-input-json file://example-start-command.json
  ```

  The following is the code of `example-start-command.json`\.

  ```
  {
      "CategoryName": "Example-Call-Analytics-Category",
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