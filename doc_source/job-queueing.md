# Job queueing<a name="job-queueing"></a>

Job queueing enables you to submit more transcription job requests than can be concurrently processed\. Without job queueing, once you reach the quota of allowed concurrent requests, you must wait until one or more requests are completed before submitting a new request\.

Job queueing is optional for transcription job requests\. Call Analytics job requests have job queueing enabled automatically\.

If you enable job queueing, Amazon Transcribe creates a queue that contains all requests that exceed your limit\. As soon as a request is completed, a new request is pulled from your queue and processed\. Queued requests are processed in a FIFO \(first in, first out\) order\.

You can add up to 10,000 jobs to your queue\. If you exceed this limit, you get a `LimitExceededConcurrentJobException` error\. To maintain optimal performance, Amazon Transcribe only uses up to 90 percent of your quota \(a bandwidth ratio of 0\.9\) to process queued jobs\. Note that this is a default value that can be increased\.

**Tip**  
You can find a list of default limits and quotas for Amazon Transcribe resources in the [Quotas](limits-guidelines.md#limits) section\. Some of these defaults can be increased upon request; refer to [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) for more information\.

If you enable job queueing but don't exceed the quota for concurrent requests, all requests are processed concurrently\.

## Enabling job queueing<a name="job-queueing-how"></a>

You can enable job queueing using the **AWS Management Console**, **AWS SDK**, or **AWS CLI**; see the following for examples:

### AWS Management Console<a name="queueing-console-batch"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select **Create job** \(top right\)\. This opens the **Specify job details** page\.

1. In the **Job Settings** box, there is an **Additional settings** panel\. If you expand this panel, you can select the **Add to job queue** box to enable job queueing\.  
![\[Amazon Transcribe console screenshot: the 'specify job details' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/jobqueueing.png)

1. Fill in any other fields you wish to include on the **Specify job details** page, then select **Next**\. This takes you to the **Configure job \- *optional* page**\.

1. Select **Create job** to run your transcription job\. 

### AWS CLI<a name="queueing-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `job-execution-settings` parameter with the `AllowDeferredExecution` sub\-parameter\. Note that when you include `AllowDeferredExecution` in your request, you must also include `DataAccessRoleArn`\.

For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [JobExecutionSettings](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_JobExecutionSettings.html)\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--output-key my-output-files/ \
--language-code en-US \
--job-execution-settings AllowDeferredExecution=true,DataAccessRoleArn=arn:aws:iam::111122223333:role/ExampleRole
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that adds subtitles to that job\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--cli-input-json file://my-first-queueing-request.json
```

The file *my\-first\-queueing\-request\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "my-first-transcription-job",
  "Media": {
        "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
  },
  "OutputBucketName": "DOC-EXAMPLE-BUCKET",
  "OutputKey": "my-output-files/", 
  "LanguageCode": "en-US",
  "JobExecutionSettings": {
        "AllowDeferredExecution": true,
        "DataAccessRoleArn": "arn:aws:iam::111122223333:role/ExampleRole"
  }
}
```

### AWS SDK for Python \(Boto3\)<a name="queueing-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to enable job queueing using the `AllowDeferredExecution` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. Note that when you include `AllowDeferredExecution` in your request, you must also include `DataAccessRoleArn`\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [JobExecutionSettings](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_JobExecutionSettings.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe using AWS SDKs](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-queueing-request"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
transcribe.start_transcription_job(
    TranscriptionJobName = job_name,
    Media = {
        'MediaFileUri': job_uri
    },
    OutputBucketName = 'DOC-EXAMPLE-BUCKET',
    OutputKey = 'my-output-files/', 
    LanguageCode = 'en-US', 
    JobExecutionSettings = {
        'AllowDeferredExecution': True,
        'DataAccessRoleArn': 'arn:aws:iam::111122223333:role/ExampleRole'
   }
)

while True:
    status = transcribe.get_transcription_job(TranscriptionJobName = job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

You can view the progress of a queued job via the AWS Management Console or by submitting a [GetTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetTranscriptionJob.html) request\. When a job is queued, the `Status` is `QUEUED`\. The status changes to `IN_PROGRESS` once your job starts processing, then changes to either `COMPLETED` or `FAILED` when processing is finished\.