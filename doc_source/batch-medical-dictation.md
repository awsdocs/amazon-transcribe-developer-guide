# Transcribing an audio file of a medical dictation<a name="batch-medical-dictation"></a>

Use a batch transcription job to transcribe audio files of medical conversations\. You can use this to transcribe a clinician\-patient dialogue\. You can start a batch transcription job in either the [ StartMedicalTranscriptionJob ](API_StartMedicalTranscriptionJob.md) API or the Amazon Transcribe Medical console\.

When you start a medical transcription job with the [ StartMedicalTranscriptionJob ](API_StartMedicalTranscriptionJob.md) API, you specify `PRIMARYCARE` as the value of the `Specialty` parameter\. 

## Console<a name="batch-med-dictation-console"></a>

**To transcribe a clinician\-patient dialogue \(console\)**

To use the console to transcribe a clinician\-patient dialogue, create a transcription job and choose **Conversation** for **Audio input type**\.

1. Sign in to the [Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, under **Job settings **, specify the following\.

   1. **Name** – the name of the transcription job\.

   1. **Audio input type** – **Dictation**

1. For the remaining fields, specify the Amazon Simple Storage Service \(Amazon S3\) location of your audio file and where you want to store the output of your transcription job\.

1. Choose **Next**\.

1. Choose **Create**\.

## API<a name="batch-med-dictation-api"></a>

**To transcribe a medical conversation using a batch transcription job \(API\)**
+ For the [ StartMedicalTranscriptionJob ](API_StartMedicalTranscriptionJob.md) API, specify the following\.

  1. For `MedicalTranscriptionJobName`, specify a name unique in your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file and the language of your vocabulary filter\.

  1. In the `MediaFileUri` parameter of the `Media` object, specify the name of the audio file that you want to transcribe\.

  1. For `Specialty`, specify the medical specialty of the clinician speaking in the audio file\.

  1. For `Type`, specify `DICTATION`\.

  1. For `OutputBucketName`, specify the Amazon Simple Storage Service \(Amazon S3\) bucket to store the transcription results\.

  The following is an example request that uses the AWS SDK for Python \(Boto3\) to transcribe a medical dictation of a clinician in the `PRIMARYCARE` specialty\.

  ```
   from __future__ import print_function
   import time
   import boto3
   transcribe = boto3.client('transcribe')
   job_name = "your-medical-conversation-transcription-job-name"
   job_uri = "s3://DOC-EXAMPLE-BUCKET1/example-audio-file.extension"
   transcribe.start_medical_transcription_job(
       MedicalTranscriptionJobName = job_name,
       Media = {'MediaFileUri': job_uri},
       LanguageCode = 'en-US',
       Specialty = 'PRIMARYCARE',
       Type = 'DICTATION',
       OutputBucketName = 'DOC-EXAMPLE-BUCKET1'
    )
  while True:
      status = transcribe.get_medical_transcription_job(MedicalTranscriptionJobName=job_name)
      if status['MedicalTranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
          break
      print("Not ready yet...")
      time.sleep(5)
  print(status)
  ```

The following example code shows the transcription results of a medical dictation\.

```
{
    "jobName": "dictation-medical-transcription-job",
    "accountId": "account-id-number",
    "results": {
        "transcripts": [
            {
                "transcript": "... came for a follow up visit today..."
            }
        ],
        "items": [
            {
            ...
                "start_time": "4.85",
                "end_time": "5.12",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "came"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.12",
                "end_time": "5.29",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "for"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.29",
                "end_time": "5.33",
                "alternatives": [
                    {
                        "confidence": "0.9955",
                        "content": "a"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.33",
                "end_time": "5.66",
                "alternatives": [
                    {
                        "confidence": "0.9754",
                        "content": "follow"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.66",
                "end_time": "5.75",
                "alternatives": [
                    {
                        "confidence": "0.9754",
                        "content": "up"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.75",
                "end_time": "6.02",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "visit"
                    }
                ]
                ...
    },
    "status": "COMPLETED"
}
```

## AWS CLI<a name="batch-med-dictation-cli"></a>

**To identify the speakers in an audio file using a batch transcription job \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-medical-transcription-job \
  --cli-input-json file://filepath/example-start-command.json
  ```

  The following code shows the contents of `example-start-command.json`\.

  ```
    {
        "MedicalTranscriptionJobName": "conversation-medical-transcription-job",        
        "LanguageCode": "en-US",
        "Specialty": "PRIMARYCARE",
        "Type": "DICTATION",
        "OutputBucketName":"DOC-EXAMPLE-BUCKET",
        "Media": {
            "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET1/example-audio-file.extension"
        }
    }
  ```

  The following is the response from running the preceding CLI command\.

  ```
  {
      "MedicalTranscriptionJob": {
          "MedicalTranscriptionJobName": "example-dictation-medical-transcription-job",
          "TranscriptionJobStatus": "IN_PROGRESS",
          "LanguageCode": "en-US",
          "Media": {
              "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET1/example-audio-file.extension"
          },
          "StartTime": "2020-09-20T00:35:22.256000+00:00",
          "CreationTime": "2020-09-20T00:35:22.218000+00:00",
          "Specialty": "PRIMARYCARE",
          "Type": "DICTATION"
      }
  }
  ```