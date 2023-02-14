# Using Amazon EventBridge with Amazon Transcribe<a name="monitoring-events"></a>

With Amazon EventBridge, you can respond to state changes in your Amazon Transcribe jobs by initiating events in other AWS services\. When a transcription job changes state, EventBridge automatically sends an event to an event stream\. You create rules that define the events that you want to monitor in the event stream and the action that EventBridge should take when those events occur\. For example, routing the event to another service \(or target\), which can then take an action\. You could, for example, configure a rule to route an event to an AWS Lambda function when a transcription job has completed successfully\.

Before using EventBridge, note the following definitions:
+ **Event** – An event indicates a change in the state of one of your transcription jobs\. For example, when the `TranscriptionJobStatus` of a job changes from `IN_PROGRESS` to `COMPLETED`\.
+ **Target** – A target is another AWS service that processes an event\. For example, AWS Lambda or Amazon Simple Notification Service \(Amazon SNS\)\. A target receives events in JSON format\.
+ **Rule** – A rule matches incoming events that you want EventBridge to watch for and routes them to a target or targets for processing\. If a rule routes an event to multiple targets, all of the targets process the event in parallel\. A rule can customize the JSON sent to the target\.

Amazon EventBridge are emitted on a best\-effort basis\. For more information about creating and managing events in EventBridge, see [Amazon EventBridge events](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-events.html) in the *Amazon EventBridge User Guide*\.

## Defining EventBridge rules<a name="defining-rules"></a>

To define EventBridge rules, use the [AWS Management Console](https://console.aws.amazon.com/events)\. When you define a rule, use Amazon Transcribe as the service name\. For an example of how to create an EventBridge rule, see [Amazon EventBridge rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-rules.html)\.

The following is an example of an EventBridge rule for Amazon Transcribe that's initiated when a transcription job's status changes to `COMPLETED` or `FAILED`\. 

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
+ `detail` – The new job status of the transcription job\. In this example, the rule initiates an event when the job status changes to `COMPLETED` or `FAILED`\. For a list of status values, see the `TranscriptionJobStatus` field of the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptionJob.html) API\.

## Amazon Transcribe events<a name="events"></a>

Amazon EventBridge logs several Amazon Transcribe events: transcription job events, automatic language identification events, Call Analytics events, and vocabulary events\.

Definitions for all fields are provided below the event examples\.

### Transcription job events<a name="job-event"></a>

When a job's state changes from `IN_PROGRESS` to either `COMPLETED` or `FAILED`, Amazon Transcribe generates an event\. To identify the job that changed state and initiate the event in your target, use the event's `TranscriptionJobName` field\. An Amazon Transcribe event contains the following information\. A `FailureReason` field is added under `detail` if your transcription job status is `FAILED`\.

```
{
    "version": "0",
    "id": "event ID",
    "detail-type":"Transcribe Job State Change",
    "source": "aws.transcribe",
    "account": "111122223333",
    "time": "timestamp",
    "region": "us-west-2",
    "resources": [ ],
    "detail": {
          "TranscriptionJobName": "my-first-transcription-job",
          "TranscriptionJobStatus": "COMPLETED"
    }   
}
```

### Language identification events<a name="lang-id-event"></a>

When you enable [automatic language identification](lang-id.md), Amazon Transcribe generates an event when the language identification state is either `COMPLETED` or `FAILED`\. To identify the job that changed state and initiate the event in your target, use the event's `JobName` field\. An Amazon Transcribe event contains the following information\. A `FailureReason` field is added under `detail` if your language identification status is `FAILED`\.

```
{
    "version": "0",
    "id": "event ID",
    "detail-type": "Language Identification State Change",
    "source": "aws.transcribe",
    "account": "111122223333",
    "time": "timestamp",
    "region": "us-west-2",
    "resources": [ ],
    "detail": {
        "JobType": "TranscriptionJob",
        "JobName": "my-first-lang-id-job",
        "LanguageIdentificationStatus": "status"
    }
}
```

### Call Analytics events<a name="analytics-event"></a>

When a [Call Analytics](call-analytics.md) job state changes from `IN_PROGRESS` to either `COMPLETED` or `FAILED`, Amazon Transcribe generates an event\. To identify the Call Analytics job that changed state and initiates the event in your target, use the event's `JobName` field\. An Amazon Transcribe event contains the following information\. A `FailureReason` field is added under `detail` if your Call Analytics job status is `FAILED`\.

```
{
    "version": "0",
    "id": "event ID",
    "detail-type": "Call Analytics Job State Change",
    "source": "aws.transcribe",
    "account": "111122223333",
    "time": "timestamp",
    "region": "us-west-2",
    "resources": [ ],
    "detail": {
        "JobName": "my-first-analytics-job",
        "JobStatus": "status"
    }
}
```

### Call Analytics post\-call events<a name="analytics-stream-event"></a>

When a [post\-call analytics](tca-post-call.md) job changes state from `IN_PROGRESS` to either `COMPLETED` or `FAILED`, Amazon Transcribe generates an event\. To identify the Call Analytics post\-call job that changed state and initiate the event in your target, use the event's `StreamingSessionId` field\.

A `COMPLETED` event contains the following information:

```
{
    "version": "0",
    "id": "event ID",
    "detail-type": "Call Analytics Post Call Job State Change",
    "source": "aws.transcribe",
    "account": "111122223333",
    "time": "timestamp",
    "region": "us-west-2",
    "resources": [ ],
    "detail": {
        "StreamingSessionId": "session-id",
        "PostCallStatus": "status",
        "Transcript": {
            "RedactedTranscriptFileUri": "s3://DOC-EXAMPLE-BUCKET/my-output-files/my-redacted-file.JSON",
            "TranscriptFileUri": "s3://DOC-EXAMPLE-BUCKET/my-output-files/my-file.JSON"
        },
        "Media": {
            "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-output-files/my-redacted-file.WAV",
            "RedactedMediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-output-files/my-redacted-file.WAV"
        }
    }
}
```

A `FAILED` event contains the following information:

```
{
    "version": "0",
    "id": "event ID",
    "detail-type": "Call Analytics Post Call Job State Change",
    "source": "aws.transcribe",
    "account": "111122223333",
    "time": "timestamp",
    "region": "us-west-2",
    "resources": [ ],
    "detail": {
        "StreamingSessionId": "session-id",
        "PostCallStatus": "status"
    }
}
```

### Vocabulary events<a name="vocab-event"></a>

When a [custom vocabulary](custom-vocabulary.md)'s state changes from `PENDING` to either `READY` or `FAILED`, Amazon Transcribe generates an event\. To identify the custom vocabulary that changed state and initiate the event in your target, use the event's `VocabularyName` field\. An Amazon Transcribe event contains the following information\. A `FailureReason` field is added under `detail` if your custom vocabulary state is `FAILED`\.

```
{
    "version": "0",
    "id": "event ID",
    "detail-type": "Vocabulary State Change",
    "source": "aws.transcribe",
    "account": "111122223333",
    "time": "timestamp",
    "region": "us-west-2",
    "resources": [ ],
    "detail": {
        "VocabularyName": "unique-vocabulary-name",
        "VocabularyState": "state"
    }
}
```

Descriptions for the preceding fields:
+ `version` – The version of the event data\. This value is always `0`\.
+ `id` – A unique identifier generated by EventBridge for the event\.
+ `detail-type` – An identifier for the details of the event\. For Amazon Transcribe, this is one of `Transcribe Job State Change`, `Language Identification State Change`, `Call Analytics Job State Change`, or `Vocabulary State Change`\.
+ `source` – The source of the event\. For Amazon Transcribe this is always `aws.transcribe`\.
+ `account` – The AWS account ID of the account that generated the API call\.
+ `timestamp` – The date and time the event is delivered\.
+ `region` – The AWS Region in which the request is made\.
+ `resources` – The resources used by the API call\. For Amazon Transcribe, this field is always empty\.
+ `detail` – Details about the event\. The fields within the `detail` tag may vary depending on the type of event, but may contain the following fields:
  + `CallAnalyticsJobName` – The unique name of your Call Analytics transcription job\.
  + `FailureReason` – This field is present if the state or status changes to `FAILED`, and describes the reason for the `FAILED` state or status\.
  + `JobStatus` – The status of your Call Analytics transcription job\. It can be either `COMPLETED` or `FAILED`\.
  + `JobType` – For transcription jobs, this value must be `TranscriptionJob`\.
  + `LanguageIdentificationStatus` – The status of language identification in a transcription job\. It can be either `COMPLETED` or `FAILED`\.
  + `StreamingSessionId` – The identification number assigned to your real\-time Call Analytics transcription request\.
  + `TranscriptionJobName` – The unique name you chose for your transcription job\.
  + `TranscriptionJobStatus ` – The status of the transcription job\. For a list of status values, see the `TranscriptionJobStatus` field of the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptionJob.html) data type\.
  + `VocabularyName` – The unique name for your custom vocabulary\.
  + `VocabularyState` – The processing state of your custom vocabulary\. For a list of status values, see the `VocabularyState` field of the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_VocabularyInfo.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_VocabularyInfo.html) data type\.