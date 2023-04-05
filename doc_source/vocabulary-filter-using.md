# Using a custom vocabulary filter<a name="vocabulary-filter-using"></a>

Once your custom vocabulary filter is created, you can include it in your transcription requests; refer to the following sections for examples\.

The language of the custom vocabulary filter you're including in your request must match the language code you specify for your media\. If you use language identification and specify multiple language options, you can include one custom vocabulary filter per specified language\. If the languages of your custom vocabulary filters don't match the language identified in your audio, your filters are not applied to your transcription and there are no warnings or errors\.

## Using a custom vocabulary filter in a batch transcription<a name="custom-vocabulary-using-batch"></a>

To use a custom vocabulary filter with a batch transcription, see the following for examples:

### AWS Management Console<a name="vocab-filter-using-console-batch"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select **Create job** \(top right\)\. This opens the **Specify job details** page\.  
![\[Amazon Transcribe console screenshot: the 'specify job settings' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-1.png)

   Name your job and specify your input media\. Optionally include any other fields, then choose **Next**\.

1. On the **Configure job** page, in the **Content removal** panel, toggle on **Vocabulary filtering**\.  
![\[Amazon Transcribe console screenshot: the 'configure job' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-configure-job-vocab-filter.png)

1. Select your custom vocabulary filter from the dropdown menu and specify the filtration method\.  
![\[Amazon Transcribe console screenshot: vocabulary filter selection options.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-vocab-filter-method.png)

1. Select **Create job** to run your transcription job\. 

### AWS CLI<a name="vocab-filter-using-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `Settings` parameter with the `VocabularyFilterName` and `VocabularyFilterMethod` sub\-parameters\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html)\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--output-key my-output-files/ \
--language-code en-US \
--settings VocabularyFilterName=my-first-vocabulary-filter,VocabularyFilterMethod=mask
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that includes your custom vocabulary filter with that job\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--cli-input-json file://my-first-vocabulary-filter-job.json
```

The file *my\-first\-vocabulary\-filter\-job\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "my-first-transcription-job",
  "Media": {
        "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
  },
  "OutputBucketName": "DOC-EXAMPLE-BUCKET",
  "OutputKey": "my-output-files/", 
  "LanguageCode": "en-US",
  "Settings": {
        "VocabularyFilterName": "my-first-vocabulary-filter",
        "VocabularyFilterMethod": "mask"
   }
}
```

### AWS SDK for Python \(Boto3\)<a name="vocab-filter-using-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to include a custom vocabulary filter using the `Settings` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe using AWS SDKs](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-transcription-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
transcribe.start_transcription_job(
    TranscriptionJobName = job_name,
    Media = {
        'MediaFileUri': job_uri
    },
    OutputBucketName = 'DOC-EXAMPLE-BUCKET',
    OutputKey = 'my-output-files/', 
    LanguageCode = 'en-US', 
    Settings = {
        'VocabularyFilterName': 'my-first-vocabulary-filter',
        'VocabularyFilterMethod': 'mask' 
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

## Using a custom vocabulary filter in a streaming transcription<a name="custom-vocabulary-using-stream"></a>

To use a custom vocabulary filter with a streaming transcription, see the following for examples:

### AWS Management Console<a name="vocab-filter-using-console-stream"></a>

1. Sign into the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\. Scroll down to **Content removal settings** and expand this field if it is minimized\.  
![\[Amazon Transcribe console screenshot: the 'real-time transcription' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/stream-main.png)

1. Toggle on **Vocabulary filtering**\. Select a custom vocabulary filter from the dropdown menu and specify the filtration method\.  
![\[Amazon Transcribe console screenshot: the expanded 'content removal settings' pane.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-filter-stream.png)

   Include any other settings you want to apply to your stream\.

1. You're now ready to transcribe your stream\. Select **Start streaming** and begin speaking\. To end your dictation, select **Stop streaming**\.

### HTTP/2 stream<a name="vocab-filter-using-http2"></a>

This example creates an HTTP/2 request that includes your custom vocabulary filter and filter method\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Setting up an HTTP/2 stream](streaming-http2.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
POST /stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
X-Amz-Target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
Content-Type: application/vnd.amazon.eventstream
X-Amz-Content-Sha256: string
X-Amz-Date: 20220208T235959Z
Authorization: AWS4-HMAC-SHA256 Credential=access-key/20220208/us-west-2/transcribe/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date;x-amz-target;x-amz-security-token, Signature=string
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000      
x-amzn-transcribe-vocabulary-filter-name: my-first-vocabulary-filter
x-amzn-transcribe-vocabulary-filter-method: mask
transfer-encoding: chunked
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

### WebSocket stream<a name="vocab-filter-using-websocket"></a>

This example creates a presigned URL that applies your custom vocabulary filter to a WebSocket stream\. Line breaks have been added for readability\. For more information on using WebSocket streams with Amazon Transcribe, see [Setting up a WebSocket stream](streaming-websocket.md)\. For more detail on parameters, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/stream-transcription-websocket?
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request
&X-Amz-Date=20220208T235959Z
&X-Amz-Expires=250
&X-Amz-Security-Token=security-token
&X-Amz-Signature=string
&X-Amz-SignedHeaders=content-type%3Bhost%3Bx-amz-date
&language-code=en-US
&media-encoding=flac
&sample-rate=16000    
&vocabulary-filter-name=my-first-vocabulary-filter
&vocabulary-filter-method=mask
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.