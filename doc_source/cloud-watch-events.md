# Using Amazon EventBridge with Amazon Transcribe<a name="cloud-watch-events"></a>

With Amazon EventBridge, you can respond to state changes in your Amazon Transcribe jobs by triggering events in other AWS services\. When a transcription job changes state, EventBridge automatically sends an event to an event stream\. You create rules that define the events that you want to monitor in the event stream and the action that EventBridge should take when those events occur\. For example, routing the event to another service \(or target\), which can then take an action\. You could, for example, configure a rule to route an event to an AWS Lambda function when a transcription job has completed successfully\.

Before using EventBridge, you should understand the following concepts:
+ **Event** – An event indicates a change in the state of one of your transcription jobs\. For example, when the `TranscriptionJobStatus` of a job changes from `IN_PROGRESS` to `COMPLETED`\.
+ **Target** – A target is another AWS service that processes an event\. For example, AWS Lambda or Amazon Simple Notification Service \(Amazon SNS\)\. A target receives events in JSON format\. 
+ **Rule** – A rule matches incoming events that you want EventBridge to watch for and routes them to a target or targets for processing\. If a rule routes an event to multiple targets, all of the targets process the event in parallel\. A rule can customize the JSON sent to the target\.

EventBridge are emitted on a best\-effort basis\. For more information about creating and managing events in EventBridge, see [What is Amazon CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html) in the *Amazon CloudWatch User Guide*\.

## Defining EventBridge rules<a name="defining-rules"></a>

To define EventBridge rules, use the [CloudWatch Events console](https://console.aws.amazon.com/cloudwatch)\. When you define a rule, use Amazon Transcribe as the service name\. For an example of how to create an EventBridge rule, see [Creating a CloudWatch Events Rule That Triggers on an Event](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/Create-CloudWatch-Events-Rule.html) in the *Amazon CloudWatch User Guide*\.

The following is an example of an EventBridge rule for Amazon Transcribe\. It's triggered when a transcription job's status changes to `COMPLETED` or `FAILED`\. 

```
{
  "source": [
    "aws.transcribe"
  ],
  "detail-type": [
    "Transcribe Job State Change"
  ],
  "detail": {
    "TranscriptionJobStatus": [
      "COMPLETED",
      "FAILED"
    ]
  }
}
```

The rule contains the following fields:
+ `source` –The source of the event\. For Amazon Transcribe, this is always `aws.transcribe`\.
+ `detail-type` – An identifier for the details of the event\. For Amazon Transcribe, this is always `Transcribe Job State Change`\.
+ `detail` – The new job status of the transcription job\. In this example, the rule triggers an event when the job status changes to `COMPLETED` or `FAILED`\. For a list of status values, see the `TranscriptionJobStatus` field of the [ TranscriptionJob ](API_TranscriptionJob.md) API\.

## Amazon Transcribe events<a name="events"></a>

Amazon CloudWatch logs three kinds of Amazon Transcribe events: transcription job events, automatic language identification events, and call analytics events\.

### Transcription job events<a name="job-event"></a>

When a job's state changes from `IN_PROGRESS` to either `COMPLETED` or `FAILED`, Amazon Transcribe generates an event\. To identify the job that changed state and triggered the event in your target, use the event's `TranscriptionJobName` field\. An Amazon Transcribe event contains the following information\.

```
 {
   "version": "0",
   "id": "event ID",
   "detail-type":"Transcribe Job State Change",
   "source": "aws.transcribe",
   "account": "account ID",
   "time": "timestamp",
   "region": "region",
   "resources": [],
   "detail": {
     "TranscriptionJobName": "job-name",
     "TranscriptionJobStatus": "status"
   }   
 }
```

### Language identification events<a name="lang-id-event"></a>

When you enable automatic language identification, Amazon Transcribe generates an event when the language identification state is either `COMPLETED` or `FAILED`\. To identify the job that changed state and triggered the event in your target, use the event's `JobName` field\. An Amazon Transcribe event contains the following information\.

```
 {
  "version": "0",
  "id": "event ID",
  "detail-type": "Language Identification State Change",
  "source": "aws.transcribe",
  "account": "account ID",
  "time": "timestamp",
  "region": "region",
  "resources": [ ],
  "detail": {
    "JobType": "TranscriptionJob",
    "JobName": "job-name",
    "LanguageIdentificationStatus": "status" 
  }
}
```

### Call analytics events<a name="analytics-event"></a>

When a call analytics job's state changes from `IN_PROGRESS` to either `COMPLETED` or `FAILED`, Amazon Transcribe generates an event\. To identify the call analytics job that changed state and triggered the event in your target, use the event's `JobName` field\. An Amazon Transcribe event contains the following information\.

```
 {
  "version": "0",
  "id": "event ID",
  "detail-type": "Call Analytics Job State Change",
  "source": "aws.transcribe",
  "account": "account ID",
  "time": "timestamp",
  "region": "region",
  "resources": [],
  "detail": {
    "JobName": "job-name",
    "JobStatus": "status"
  }
}
```

Descriptions for the fields listed above:
+ `version` – The version of the event data\. This value is always `0`\.
+ `id` – A unique identifier generated by CloudWatch Events for the event\.
+ `detail-type` – An identifier for the details of the event\. For Amazon Transcribe, this is either `Transcribe Job State Change`, `Language Identification State Change`, or `Call Analytics Job State Change`\.
+ `source` – The source of the event\. For Amazon Transcribe this is always `aws.transcribe`\.
+ `account ID` – The AWS account ID of the account that generated the API call\.
+ `timestamp` – The date and time that the API call was made\.
+ `region` – The AWS Region where the API call was made\.
+ `resources` – The resources used by the API call\. For Amazon Transcribe, this field is always empty\.
+ `detail` – Details about the event\. The fields within the `detail`tag may vary depending on the type of event, but may contain the following fields:
  + `JobType` – Enables reusing the event for transcription jobs\.
  + `JobName` – The unique name that you gave the transcription job\. 
  + `JobStatus` – The status of your call analytics transcription job\. It can be either `COMPLETED` or `FAILED`\.
  + `TranscriptionJobName` – The unique name that you gave the job\.
  + `TranscriptionJobStatus ` – The new status of the transcription job\. For a list of status values, see the `TranscriptionJobStatus` field of the [ TranscriptionJob ](API_TranscriptionJob.md) API\.
  + `LanguageIdentificationStatus` – The status of language identification in a transcription job\. It can be either `COMPLETED` or `FAILED`\.