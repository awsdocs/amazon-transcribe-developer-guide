# Identifying PHI in an audio file<a name="phi-id-batch"></a>

Use a batch transcription job to transcribe audio files and identify the personal health information \(PHI\) within them\. When you activate Personal Health Information \(PHI\) Identification, Amazon Transcribe Medical labels the PHI that it identified in the transcription results\. For information about the PHI that Amazon Transcribe Medical can identify, see [Identifying personal health information \(PHI\) in a transcription](phi-id.md)\.

You can start a batch transcription job using either the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API or the AWS Management Console\.

## AWS Management Console<a name="batch-med-phi-console"></a>

To use the AWS Management Console to transcribe a clinician\-patient dialogue, create a transcription job and choose **Conversation** for **Audio input type**\.

**To transcribe an audio file and identify its PHI \(AWS Management Console\)**

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, under **Job settings **, specify the following\.

   1. **Name** – The name of the transcription job that is unique to your AWS account\.

   1. **Audio input type** – **Conversation** or **Dictation**\.

1. For the remaining fields, specify the Amazon S3 location of your audio file and where you want to store the output of your transcription job\.

1. Choose **Next**\.

1. Under **Audio settings**, choose **PHI Identification**\.

1. Choose **Create**\.

## API<a name="batch-med-phi-api"></a>

**To transcribe an audio file and identify its PHI using a batch transcription job \(API\)**
+ For the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API, specify the following\.

  1. For `MedicalTranscriptionJobName`, specify a name that is unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file\.

  1. For the `MediaFileUri` parameter of the `Media` object, specify the name of the audio file that you want to transcribe\.

  1. For `Specialty`, specify the medical specialty of the clinician speaking in the audio file as `PRIMARYCARE`\.

  1. For `Type`, specify either `CONVERSATION` or `DICTATION`\.

  1. For `OutputBucketName`, specify the Amazon S3 bucket where you want to store the transcription results\.

  The following is an example request that uses the AWS SDK for Python \(Boto3\) to transcribe an audio file and identify the PHI of a patient\.

  ```
  from __future__ import print_function
  import time
  import boto3
  transcribe = boto3.client('transcribe')
  job_name = "my-first-transcription-job"
  job_uri = "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-audio-file.flac"
  transcribe.start_medical_transcription_job(
        MedicalTranscriptionJobName = job_name,
        Media = {'MediaFileUri': job_uri},
        LanguageCode = 'en-US',
        ContentIdentificationType = 'PHI',
        Specialty = 'PRIMARYCARE',
        Type = 'type', # Specify 'CONVERSATION' for a medical conversation. Specify 'DICTATION' for a medical dictation.
        OutputBucketName = 'DOC-EXAMPLE-BUCKET'
    )
  while True:
      status = transcribe.get_medical_transcription_job(MedicalTranscriptionJobName = job_name)
      if status['MedicalTranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
          break
      print("Not ready yet...")
      time.sleep(5)
  print(status)
  ```

The following example code shows the transcription results with patient PHI identified\.

```
{
    "jobName": "my-medical-transcription-job-name",
    "accountId": "111122223333",
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
  --medical-transcription-job-name my-medical-transcription-job-name\
  --language-code en-US \
  --media MediaFileUri="s3://DOC-EXAMPLE-BUCKET/my-input-files/my-audio-file.flac" \
  --output-bucket-name DOC-EXAMPLE-BUCKET \
  --specialty PRIMARYCARE \
  --type type \ # Choose CONVERSATION to transcribe a medical conversation. Choose DICTATION to transcribe a medical dictation.
  --content-identification-type PHI
  ```