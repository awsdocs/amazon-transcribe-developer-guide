# Generating alternative transcriptions<a name="alternative-med-transcriptions"></a>

When you use Amazon Transcribe Medical, you get the transcription that has the highest confidence level\. However, you can configure Amazon Transcribe Medical to return additional transcriptions with lower confidence levels\.

Use alternative transcriptions to see different interpretations of the transcribed audio\. For example, in an application that enables a person to review the transcription, you can present the alternative transcriptions for the person to choose from\.

You can generate alternative transcriptions with the AWS Management Console or the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API\.

## AWS Management Console<a name="alternative-med-transcriptions-console"></a>

To use the AWS Management Console to generate alternative transcriptions, you enable alternative results when you configure your job\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Alternative results**\.

1. For **Maximum alternatives**, enter an integer value between 2 and 10, for the maximum number of alternative transcriptions you want in the output\.

1. Choose **Create**\.

## API<a name="alternative-med-transcriptions-api"></a>

**To separate text per speaker in an audio file using a batch transcription job \(API\)**
+ For the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API, specify the following\.

  1. For `MedicalTranscriptionJobName`, specify a name that is unique in your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file and the language of your vocabulary filter\.

  1. In the `MediaFileUri` parameter of the `Media` object, specify the location of the audio file you want to transcribe\.

  1. For `Specialty`, specify the medical specialty of the clinician speaking in the audio file\.

  1. For `Type`, specify whether you're transcribing a medical conversation or a dictation\.

  1. For `OutputBucketName`, specify the Amazon S3 bucket to store the transcription results\.

  1. For the `Settings` object, specify the following\.

     1. `ShowAlternatives` – `true`\.

     1. `MaxAlternatives` \- An integer between 2 and 10 to indicate the number of alternative transcriptions you want in the transcription output\.

The following request uses the AWS SDK for Python \(Boto3\) to start a transcription job that generates up to two alternative transcriptions\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-transcription-job"
job_uri = s3://DOC-EXAMPLE-BUCKET/my-input-files/my-audio-file.flac
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
        'ShowAlternatives': True,
        'MaxAlternatives': 2
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

## AWS CLI<a name="alternative-med-transcriptions-cli"></a>

**To transcribe an audio file of a conversation between a primary care clinician and a patient in an audio file \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-transcription-job \
  --cli-input-json file://filepath/example-start-command.json
  ```

  The following code shows the contents of `example-start-command.json`\.

  ```
  >
  {
        "MedicalTranscriptionJobName": "my-first-transcription-job",
        "LanguageCode": "en-US",
        "Specialty": "PRIMARYCARE",
        "Type": "CONVERSATION",
        "OutputBucketName":"DOC-EXAMPLE-BUCKET",
        "Media": {
            "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-audio-file.flac"
          },
        "Settings":{
            "ShowAlternatives": true,
            "MaxAlternatives": 2
          }
  }
  ```