# Transcribing an audio file using a medical custom vocabulary<a name="start-med-custom-vocab-job"></a>

Use the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) or the AWS Management Console to start a transcription job that uses a custom vocabulary to improve transcription accuracy\.

## AWS Management Console<a name="start-med-custom-vocab-job-console"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Under **Customization**, enable **Custom vocabulary**\.

1. Under **Vocabulary selection**, choose a custom vocabulary\.

1. Choose **Create**\.

## API<a name="start-med-custom-vocab-api"></a>

**To enable speaker partitioning in an audio file using a batch transcription job \(API\)**
+ For the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API, specify the following\.

  1. For `MedicalTranscriptionJobName`, specify a name that is unique in your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file and the language of your vocabulary filter\.

  1. For the `MediaFileUri` parameter of the `Media` object, specify the name of the audio file that you want to transcribe\.

  1. For `Specialty`, specify the medical specialty of the clinician speaking in the audio file\.

  1. For `Type`, specify whether the audio file is a conversation or a dictation\.

  1. For `OutputBucketName`, specify the Amazon S3 bucket to store the transcription results\.

  1. For the `Settings` object, specify the following\.

     1. `VocabularyName` – the name of your custom vocabulary\.

The following request uses the AWS SDK for Python \(Boto3\) to start a batch transcription job with a custom vocabulary\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-med-transcription-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
transcribe.start_medical_transcription_job(
   MedicalTranscriptionJobName = job_name,
   Media = {
       'MediaFileUri': job_uri
   },
   OutputBucketName = 'DOC-EXAMPLE-BUCKET',
   OutputKey = 'my-output-files/', 
   LanguageCode = 'en-US',
   Specialty = 'PRIMARYCARE',
   Type = 'CONVERSATION',
   Settings = {
       'VocabularyName': 'example-med-custom-vocab'
       }
 )

while True:
   status = transcribe.get_medical_transcription_job(MedicalTranscriptionJobName = job_name)
   if status['MedicalTranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```