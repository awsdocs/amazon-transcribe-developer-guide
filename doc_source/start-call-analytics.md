# Setting up call analytics transcription jobs<a name="start-call-analytics"></a>

To get analytics data, you must run call analytics jobs\. Call analytics jobs not only transcribe the audio of the recordings between your agents and customers, but they provide meaningful information \(in the form of *analytics*\) about these conversations\. If you choose not to create any categories before running a call analytics job, the output only includes the following information:
+ Detected customer issues
+ Sentiment of the agent and the customer
+ Non\-talk time
+ Interruptions
+ Speaking volume

If you create categories, you can flag your analytics job based on the conversational characteristics you define\. These conversational characteristics can include:
+ Customer or agent sentiment during specific periods of time
+ Matching a portion of the transcript to a phrase you've specified
+ The customer or agent interrupting the other person
+ Neither the customer nor the agent spoke for a defined period of time

Once you create categories, Amazon Transcribe flags your call analytics jobs with a label indicating that the call matches all the rules you've defined in a given category\. For more information on creating categories, see [Using categories and rules](create-categories.md)\.

**Note**  
Call analytics jobs can't be classified retroactively with categories\. Only the categories you created *before* running a call analytics job can be applied to that job\.

To start a call analytics job, you can use the **Amazon Transcribe Console**, **AWS CLI**, or **AWS SDK**; see below for instructions:

## Console<a name="analytics-start-console"></a>

Use the following procedure to start a call analytics job\. The calls that match all characteristics defined by a category are labeled with that category\.

1. In the navigation pane, under Amazon Transcribe Call Analytics, choose **Call analytics jobs**\.

1. Choose **Create job**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start.png)

1. On the **Specify job details** page, provide information about your call analytics job, including the location of your input data\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start-settings1.png)

   Specify the desired S3 location of your output data and which IAM role to use\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start-settings2.png)

1. Choose **Next**\.

1. For **Configure job**, turn on any optional features you want to include with your call analytics job\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start-configure.png)

1. Choose **Create job**\.

## AWS SDK for Python \(Boto3\)<a name="analytics-start-sdk"></a>

The following example uses the AWS SDK for Python \(Boto3\) to start a call analytics job using the [start\_call\_analytics\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_call_analytics_job) method:

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "your-call-analytics-job-name"
job_uri = "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
output_location = "s3://your-S3-bucket/S3-prefix/"
data_access_role = "arn:aws:iam::account-id:role/your-IAM-role"
transcribe.start_call_analytics_job(
     CallAnalyticsJobName=job_name,
     Media={'MediaFileUri': job_uri},
     DataAccessRoleArn=data_access_role,
     OutputLocation=output_location,
     ChannelDefinitions=[{'ChannelId': 0, 'ParticipantRole': 'AGENT'},{'ChannelId': 1, 'ParticipantRole': 'CUSTOMER'}]
     )
 while True:
   status = transcribe.get_call_analytics_job(CallAnalyticsJobName=job_name)
   if status['CallAnalyticsJob']['CallAnalyticsJobStatus'] in ['COMPLETED', 'FAILED']:
     break
   print("Not ready yet...")
   time.sleep(5)
 print(status)
```

## AWS CLI<a name="analytics-start-cli"></a>

This example uses the [start\-call\-analytics\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-call-analytics-job.html) command and `channel-definitions` parameter\.

```
aws transcribe start-call-analytics-job \
--call-analytics-job-name your-job-name \
--media MediaFileUri=s3://your-S3-bucket/S3-prefix/your-filename.file-extension \
--language-code en-US \
--data-access-role-arn "arn:aws:iam::accountId:role/your-IAM-role" \
--channel-definitions '[{"ChannelId": 0, "ParticipantRole": "AGENT"},{"ChannelId": 1, "ParticipantRole": "CUSTOMER"}]'
```

Here's another example using the [start\-call\-analytics\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-call-analytics-job.html) command, and a request body that identifies audio channels for that job\.

```
aws transcribe start-call-analytics-job \
--cli-input-json file://filepath/example-start-command.json
```

The file *example\-start\-command\.json* contains the following request body\.

```
{
   "CallAnalyticsJobName": "Example-Call-Analytics-Job",
      "OutputLocation": "s3://your-S3-bucket/",
      "DataAccessRoleArn": "arn:aws:iam::accountId:role/your-IAM-role",
      "Media": {
          "MediaFileUri": "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
      },
      "ChannelDefinitions": [
          {
              "ChannelId": 0,
              "ParticipantRole": "AGENT"
          },
          {
              "ChannelId": 1,
              "ParticipantRole": "CUSTOMER"
          }
      ]
}
```