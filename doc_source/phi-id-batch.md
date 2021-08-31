# Identifying PHI in an audio file<a name="phi-id-batch"></a>

Use a batch transcription job to transcribe audio files and identify the personal health information \(PHI\) within them\. When you activate Personal Health Information \(PHI\) Identification, Amazon Transcribe Medical labels the PHI that it identified in the transcription results\. For information about the PHI that Amazon Transcribe Medical can identify, see [Identifying personal health information \(PHI\) in a transcription](phi-id.md)\.

You can start a batch transcription job using either the [ StartMedicalTranscriptionJob ](API_StartMedicalTranscriptionJob.md) API or the Amazon Transcribe Medical console\.

## Console<a name="batch-med-phi-console"></a>

To use the console to transcribe a clinician\-patient dialogue, create a transcription job and choose **Conversation** for **Audio input type**\.

**To transcribe an audio file and identify its PHI \(console\)**

1. Sign in to the [ Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, under **Job settings **, specify the following\.

   1. **Name** – The name of the transcription job that is unique to your AWS account\.

   1. **Audio input type** – **Conversation** or **Dictation**\.

1. For the remaining fields, specify the Amazon Simple Storage Service \(Amazon S3\) location of your audio file and where you want to store the output of your transcription job\.

1. Choose **Next**\.

1. Under **Audio settings**, choose **PHI Identification**\.

1. Choose **Create**\.

## API<a name="batch-med-phi-api"></a>

**To transcribe an audio file and identify its PHI using a batch transcription job \(API\)**
+ For the [ StartMedicalTranscriptionJob ](API_StartMedicalTranscriptionJob.md) API, specify the following\.

  1. For `MedicalTranscriptionJobName`, specify a name that is unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file and the language of your vocabulary filter\.

  1. For the `MediaFileUri` parameter of the `Media` object, specify the name of the audio file that you want to transcribe\.

  1. For `Specialty`, specify the medical specialty of the clinician speaking in the audio file as `PRIMARYCARE`\.

  1. For `Type`, specify either `CONVERSATION` or `DICTATION`\.

  1. For `OutputBucketName`, specify the Amazon Simple Storage Service \(Amazon S3\) bucket where you want to store the transcription results\.

  The following is an example request that uses the AWS SDK for Python \(Boto3\) to transcribe an audio file and identify the PHI of a patient\.

  ```
  from __future__ import print_function
  import time
  import boto3
  transcribe = boto3.client('transcribe')
  job_name = "medical-conversation-transcription-job-name"
  job_uri = "s3://DOC-EXAMPLE-BUCKET1/example-audio-file.extension"
  transcribe.start_medical_transcription_job(
        MedicalTranscriptionJobName = job_name,
        Media = {'MediaFileUri': job_uri},
        LanguageCode = 'en-US',
        ContentIdentificationType = 'PHI',
        Specialty = 'PRIMARYCARE',
        Type = 'type', # Specify 'CONVERSATION' for a medical conversation. Specify 'DICTATION' for a medical dictation.
        OutputBucketName = 'DOC-EXAMPLE-BUCKET2'
    )
  while True:
      status = transcribe.get_medical_transcription_job(MedicalTranscriptionJobName=job_name)
      if status['MedicalTranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
          break
      print("Not ready yet...")
      time.sleep(5)
  print(status)
  ```

The following example code shows the transcription results with patient PHI identified\.

```
{
    "jobName": "transcription-job-name",
    "accountId": "account-id",
    "results": {
        "transcripts": [{
            "transcript": "The patient's name is Bertrand."
        }],
        "items": [{
            "start_time": "0.0",
            "end_time": "0.37",
            "alternatives": [{
                "confidence": "0.9993",
                "content": "The"
            }],
            "type": "pronunciation"
        }, {
            "start_time": "0.37",
            "end_time": "0.44",
            "alternatives": [{
                "confidence": "0.9981",
                "content": "patient's"
            }],
            "type": "pronunciation"
        }, {
            "start_time": "0.44",
            "end_time": "0.52",
            "alternatives": [{
                "confidence": "1.0",
                "content": "name"
            }],
            "type": "pronunciation"
        }, {
            "start_time": "0.52",
            "end_time": "0.92",
            "alternatives": [{
                "confidence": "1.0",
                "content": "is"
            }],
            "type": "pronunciation"
        }, {
            "start_time": "0.92",
            "end_time": "0.9989",
            "alternatives": [{
                "confidence": "1.0",
                "content": "Bertrand"
            }],
            "type": "pronunciation"
        }, {
            "alternatives": [{
                "confidence": "0.0",
                "content": "."
            }],
            "type": "punctuation"
        }],
        "entities": [{
            "content": "Bertrand",
            "category": "PHI*-Personal*",
            "startTime": 0.92,
            "endTime": 1.2,
            "confidence": 0.9989
        }],
    },
    "status": "COMPLETED"
}
```

## AWS CLI<a name="batch-med-conversation-cli"></a>

**To transcribe an audio file and identify PHI using a batch transcription job \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-medical-transcription-job \
  --medical-transcription-job-name job-name\
  --language-code en-US \
  --media MediaFileUri=s3://DOC-EXAMPLE-BUCKET1/example-audio-file.extension \
  --output-bucket-name DOC-EXAMPLE-BUCKET2 \
  --specialty PRIMARYCARE \
  --type type \ # Choose CONVERSATION to transcribe a medical conversation. Choose DICTATION to transcribe a medical dictation.
  --content-identification-type PHI
  ```

  The following is the response from running the preceding CLI command\.

  ```
  {
      "MedicalTranscriptionJob": {
          "MedicalTranscriptionJobName": "job-name",
          "TranscriptionJobStatus": "IN_PROGRESS",
          "LanguageCode": "en-US",
          "Media": {
              "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET1/example-audio-file.extension"
          },
          "StartTime": "2021-04-27T22:21:52.505000+00:00",
          "CreationTime": "2021-04-27T22:21:52.459000+00:00",
          "ContentIdentificationType": "PHI",
          "Specialty": "PRIMARYCARE",
          "Type": "type"
      }
  }
  ```