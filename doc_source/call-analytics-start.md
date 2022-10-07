# Starting a Call Analytics job<a name="call-analytics-start"></a>

Before running a Call Analytics transcription job, you must create all the [categories](call-analytics-create-categories.md) you want Amazon Transcribe to match in your audio\.

**Note**  
Call Analytics jobs can't be retroactively matched to new categories\. Only the categories you create *before* running a Call Analytics job can be applied to that job\.

If you've created one or more categories, and your audio matches all the rules within at least one of your categories, Amazon Transcribe flags your output with the matching category\. If you choose not to use categories, or if your audio doesn't match the rules specified in your categories, your transcript isn't flagged\.

To start a Call Analytics job, you can use the **AWS Management Console**, **AWS CLI**, or **AWS SDK**; see the following for examples:

## AWS Management Console<a name="analytics-start-console-batch"></a>

Use the following procedure to start a Call Analytics job\. The calls that match all characteristics defined by a category are labeled with that category\.

1. In the navigation pane, under Amazon Transcribe Call Analytics, choose **Call analytics jobs**\.

1. Choose **Create job**\.  
![\[Create a new Call Analytics job from the Call Analytics jobs main page in the Amazon Transcribe console.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start.png)

1. On the **Specify job details** page, provide information about your Call Analytics job, including the location of your input data\.  
![\[The job settings are listed on the specify job details page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start-settings1.png)

   Specify the desired Amazon S3 location of your output data and which IAM role to use\.  
![\[You must specify an IAM role in the access permissions panel.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start-settings2.png)

1. Choose **Next**\.

1. For **Configure job**, turn on any optional features you want to include with your Call Analytics job\.  
![\[All of your categories are listed in the Categories pane on the configure job page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/analytics-start-configure.png)

1. Choose **Create job**\.

## AWS CLI<a name="analytics-start-cli"></a>

This example uses the [start\-call\-analytics\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-call-analytics-job.html) command and `channel-definitions` parameter\. For more information, see [StartCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html) and [ChannelDefinition](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ChannelDefinition.html)\.

```
aws transcribe start-call-analytics-job \
--region us-west-2 \
--call-analytics-job-name my-first-call-analytics-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac \
--output-location s3://DOC-EXAMPLE-BUCKET/my-output-files/ \
--data-access-role-arn arn:aws:iam::111122223333:role/ExampleRole \
--channel-definitions ChannelId=0,ParticipantRole=AGENT ChannelId=1,ParticipantRole=CUSTOMER
```

Here's another example using the [start\-call\-analytics\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-call-analytics-job.html) command, and a request body that identifies audio channels for that job\.

```
aws transcribe start-call-analytics-job \
--region us-west-2 \
--cli-input-json file://filepath/my-call-analytics-job.json
```

The file *my\-call\-analytics\-job\.json* contains the following request body\.

```
{
      "CallAnalyticsJobName": "my-first-call-analytics-job",
      "DataAccessRoleArn": "arn:aws:iam::111122223333:role/ExampleRole",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
      },
      "OutputLocation": "s3://DOC-EXAMPLE-BUCKET/my-output-files/",
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

## AWS SDK for Python \(Boto3\)<a name="analytics-start-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to start a Call Analytics job using the [start\_call\_analytics\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_call_analytics_job) method\. For more information, see [StartCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html) and [ChannelDefinition](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ChannelDefinition.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe using AWS SDKs](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-call-analytics-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
output_location = "s3://DOC-EXAMPLE-BUCKET/my-output-files/"
data_access_role = "arn:aws:iam::111122223333:role/ExampleRole"
transcribe.start_call_analytics_job(
     CallAnalyticsJobName = job_name,
     Media = {
        'MediaFileUri': job_uri
     },
     DataAccessRoleArn = data_access_role,
     OutputLocation = output_location,
     ChannelDefinitions = [
        {
            'ChannelId': 0, 
            'ParticipantRole': 'AGENT'
        },
        {
            'ChannelId': 1, 
            'ParticipantRole': 'CUSTOMER'
        }
     ]
)
    
 while True:
   status = transcribe.get_call_analytics_job(CallAnalyticsJobName = job_name)
   if status['CallAnalyticsJob']['CallAnalyticsJobStatus'] in ['COMPLETED', 'FAILED']:
     break
   print("Not ready yet...")
   time.sleep(5)
 print(status)
```