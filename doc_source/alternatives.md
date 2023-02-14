# Alternative transcriptions<a name="alternatives"></a>

When Amazon Transcribe transcribes audio, it creates different versions of the same transcript and assigns a confidence score to each version\. In a typical transcription, you only get the version with the highest confidence score\.

If you enable alternative transcriptions, Amazon Transcribe returns other versions of your transcript that have lower confidence levels\. You can choose to have up to ten alternative transcriptions returned\. If you specify a greater number of alternatives than what Amazon Transcribe identifies, only the actual number of alternatives is returned\.

All alternatives are located in the same transcription output file and are presented at the segment level\. Segments are natural pauses in speech, such as a change in speaker or a pause in the audio\.

Alternative transcriptions are only available for batch transcriptions\.

Your transcription output is structured as follows\. The ellipses \(*\.\.\.*\) in the code examples indicate where content has been removed for brevity\.

1. A complete final transcription for a given segment\.

   ```
   "results": {
       "language_code": "en-US",
       "transcripts": [
           {
               "transcript": "The amazon is the largest rainforest on the planet."
           }
       ],
   ```

1. A confidence score for each word in the preceding `transcript` section\.

   ```
   "items": [
       {
           "start_time": "1.15",
           "end_time": "1.35",
           "alternatives": [
               {
                   "confidence": "1.0",
                   "content": "The"
               }
           ],
           "type": "pronunciation"
       },
       {
           "start_time": "1.35",
           "end_time": "2.05",
           "alternatives": [
               {
                   "confidence": "1.0",
                   "content": "amazon"
               }
           ],
           "type": "pronunciation"
       },
   ```

1. Your alternative transcriptions are located in the `segments` portion of your transcription output\. The alternatives for each segment are ordered by descending confidence score\.

   ```
   "segments": [
               {
                   "start_time": "1.04",
                   "end_time": "5.065",
                   "alternatives": [
                       {    
                   ...
                           "transcript": "The amazon is the largest rain forest on the planet.",
                           "items": [
                               {
                                "start_time": "1.15",
                                   "confidence": "1.0",
                                   "end_time": "1.35",
                                   "type": "pronunciation",
                                   "content": "The"
                               },
                               ...
                               {
                                   "start_time": "3.06",
                                   "confidence": "0.0037",
                                   "end_time": "3.38",
                                   "type": "pronunciation",
                                   "content": "rain"
                               },
                               {
                                   "start_time": "3.38",
                                   "confidence": "0.0037",
                                   "end_time": "3.96",
                                   "type": "pronunciation",
                                   "content": "forest"
                               },
   ```

1. A status at the end of your transcription output\.

   ```
   "status": "COMPLETED"
   }
   ```

## Requesting alternative transcriptions<a name="how-alternatives-how-to"></a>

You can request alternative transcriptions using the **AWS Management Console**, **AWS CLI**, or **AWS SDKs**; see the following for examples:

### AWS Management Console<a name="alt-transcription-console-batch"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select **Create job** \(top right\)\. This opens the **Specify job details** page\.  
![\[Amazon Transcribe console 'Specify job details' page. In the 'Job settings' panel, you can specify a name for your transcription job, select a Model type, and specify your language settings.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-1.png)![\[Amazon Transcribe console 'Specify job details' page. In the 'Job settings' panel, you can specify a name for your transcription job, select a Model type, and specify your language settings.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. Fill in any fields you want to include on the **Specify job details** page, then select **Next**\. This takes you to the **Configure job \- *optional*** page\.

   Select **Alternative results** and specify the maximum number of alternative transcription result you want in your transcript\.  
![\[Amazon Transcribe console 'Configure job' page. In the 'Audio settings' panel, you can enable Alternative results and specify the maximum number of alternatives you want included in your transcription output.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/alt-transcription-configure-batch.png)

1. Select **Create job** to run your transcription job\. 

### AWS CLI<a name="alt-transcription-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `ShowAlternatives` parameter\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html#transcribe-Type-Settings-ShowAlternatives](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html#transcribe-Type-Settings-ShowAlternatives)\.

Note that if you include `ShowAlternatives=true` in your request, you must also include `MaxAlternatives`\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--output-key my-output-files/ \
--language-code en-US \
--settings ShowAlternatives=true,MaxAlternatives=4
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that includes alternative transcriptions\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--cli-input-json file://filepath/my-first-alt-transcription-job.json
```

The file *my\-first\-alt\-transcription\-job\.json* contains the following request body\.

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
        "ShowAlternatives": true,
        "MaxAlternatives": 4
   }
}
```

### AWS SDK for Python \(Boto3\)<a name="alt-transcription-python-batch"></a>

The following example uses the AWS SDK for Python \(Boto3\) to request alternative transcriptions by using the `ShowAlternatives` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html#transcribe-Type-Settings-ShowAlternatives](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html#transcribe-Type-Settings-ShowAlternatives)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe using AWS SDKs](service_code_examples.md) chapter\.

Note that if you include `'ShowAlternatives':True` in your request, you must also include `MaxAlternatives`\.

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
        'ShowAlternatives':True, 
        'MaxAlternatives':4
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