# Generating alternative transcriptions<a name="alternative-med-transcriptions"></a>

When you use Amazon Transcribe Medical, you get the transcription that has the highest confidence level\. However, you can configure Amazon Transcribe Medical to return additional transcriptions with lower confidence levels\.

Use alternative transcriptions to see different interpretations of the transcribed audio\. For example, in an application that enables a person to review the transcription, you can present the alternative transcriptions for the person to choose from\.

You can generate alternative transcriptions with the Amazon Transcribe Medical console or the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation\.

## Console<a name="alternative-med-transcriptions-console"></a>

**To generate additional alternative transcriptions in a transcription job \(console\)**

To use the console to generate alternative transcriptions, you enable alternative results when you configure your job\.

1. Sign in to AWS Management Console and open the Amazon Transcribe Medical console at [Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Alternative results**\.

1. For **Maximum alternatives**, enter an integer value between 2 and 10, for the maximum number of alternative transcriptions you want in the output\.

1. Choose **Create**\.

## API<a name="alternative-med-transcriptions-api"></a>

**To identify speakers in an audio file using a batch transcription job \(API\)**
+  In the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation, specify the following\.

  1. For `MedicalTranscriptionJobName`, specify a name that is unique in your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file and the language of your vocabulary filter\.

  1. In the `MediaFileUri` parameter of the `Media` object, specify the name of the audio file that you want to transcribe\.

  1. For `Specialty`, specify the medical specialty of the clinician speaking in the audio file\.

  1. For `Type`, specify whether you're transcribing a medical conversation or a dictation\.

  1. For `OutputBucketName`, specify the Amazon Simple Storage Service \(Amazon S3\) bucket to store the transcription results\.

  1. For the `Settings` object, specify the following\.

     1. `ShowAlternatives` – `true`\.

     1. `MaxAlternatives` \- An integer between 2 and 10 to indicate the number of alternative transcriptions that you want in the transcription output\.

The following request uses the AWS SDK for Python \(Boto3\) to start a transcription job that generates up to two alternative transcriptions\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "your-transcription-job-name"
job_uri = s3://DOC-EXAMPLE-BUCKET1/example-audio-file.extension
transcribe.start_medical_transcription_job(
    MedicalTranscriptionJobName=job_name,
    Media = {'MediaFileUri': job_uri},
    LanguageCode = 'en-US',
    Specialty = 'PRIMARYCARE',
    Type = 'type', # Specify 'CONVERSATION' for a medical conversation. Specify 'DICTATION' for a medical dictation.
    OutputBucketName = 'Amazon-S3-bucket-name-storing-your-transcription-results'
  ),
Settings = {'ShowAlternatives': True,
       'MaxAlternatives': 2
        }
while True:
   status = transcribe.get_medical_transcription_job(MedicalTranscriptionJobName=job_name)
   if status['MedicalTranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
       break
   print("Not ready yet...")
   time.sleep(5)
print(status)
```

## AWS CLI<a name="alternative-med-transcriptions-cli"></a>

**To transcribe an audio file of a conversation between a primary care clinician and a patient in an audio file and identify what each person said in the transcription output \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-transcription-job \
  --cli-input-json file://example-start-command.json
  ```

  The following code shows the contents of `example-start-command.json`\.

  ```
  {
        "MedicalTranscriptionJobName": "alternatives-conversation-medical-transcription-job",
        "LanguageCode": "en-US",
        "Specialty": "PRIMARYCARE",
        "Type": "CONVERSATION",
        "OutputBucketName":"DOC-EXAMPLE-BUCKET",
        "Media": {
            "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file.extension"
          },
        "Settings":{
            "ShowAlternatives": true,
            "MaxAlternatives": 2
          }
  }
  ```

  The following is the response from running the preceding CLI command\.

  ```
  {
      "MedicalTranscriptionJob": {
          "MedicalTranscriptionJobName": "alternatives-medical-transcription-job",
          "TranscriptionJobStatus": "IN_PROGRESS",
          "LanguageCode": "en-US",
          "Media": {
              "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file.extension"
          },
          "StartTime": "2020-09-21T19:09:18.199000+00:00",
          "CreationTime": "2020-09-21T19:09:18.171000+00:00",
          "Settings": {
              "ShowAlternatives": true,
              "MaxAlternatives": 2
          },
          "Specialty": "PRIMARYCARE",
          "Type": "CONVERSATION"
      }
  }
  ```