# Identifying speakers and labeling their speech in audio files<a name="conversation-diarization-batch-med"></a>

You can enable speaker identification in a batch transcription job using either the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) API or the Amazon Transcribe Medical console\. This enables you to identify the speakers in a clinician\-patient conversation and determine who said what in the transcription output\.

## Console<a name="conversation-diarization-batch-med-console"></a>

**To enable speaker diarization in a transcription job \(console\)**

To use the console to enable speaker diarization in your transcription job, you enable audio identification and then speaker identification\.

1. Sign in to the [ Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Audio identification**\.

1. For **Audio identification type**, choose **Speaker identification**\.

1. For **Maximum number of speakers**, enter the maximum number of speakers that you think are speaking in your audio file\. For best results, match the number of speakers that you ask to identify to the number of speakers in the input audio\. If you specify a value less than the number of speakers in your input audio, the transcription text of the most similar sounding speakers are attributed to a speaker label\. 

1. Choose **Create**\.

## API<a name="conversation-diarization-batch-med-api"></a>

**To identify speakers in an audio file using a batch transcription job \(API\)**
+ For the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) API, specify the following\.

  1. For `MedicalTranscriptionJobName`, specify a name that is unique in your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in the audio file\.

  1. For the `MediaFileUri` parameter of the `Media` object, specify the name of the audio file that you want to transcribe\.

  1. For `Specialty`, specify the medical specialty of the clinician speaking in the audio file\.

  1. For `Type`, specify `CONVERSATION`\.

  1. For `OutputBucketName`, specify the Amazon Simple Storage Service \(Amazon S3\) bucket to store the transcription results\.

  1. For the `Settings` object, specify the following\.

     1. `ShowSpeakerLabels` – `true`\.

     1. `MaxSpeakerLabels` – An integer between 2 and 10 to indicate the number of speakers that you think are speaking in your audio\. For best results, match the number of speakers that you ask to identify to the number of speakers in the input audio\. If you specify a value less than the number of speakers in your input audio, the transcription text of the most similar sounding speakers are attributed to the same speaker label\. 

The following request uses the AWS SDK for Python \(Boto3\) to start a batch transcription job of a primary care clinician patient dialogue with speaker identification enabled\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "example-diarization-transcription"
job_uri = "https://DOC-EXAMPLE-BUCKET1.s3-Region.amazonaws.com/example-file.mp4"
transcribe.start_medical_transcription_job(
    MedicalTranscriptionJobName=job_name,
    Media = {'MediaFileUri': job_uri},
    LanguageCode = 'en-US',
    Specialty = 'PRIMARYCARE',
    Type = 'CONVERSATION',
    OutputBucketName = 'DOC-EXAMPLE-BUCKET2',
Settings = {'ShowSpeakerLabels': True,
         'MaxSpeakerLabels': 2
         }
         )
while True:
    status = transcribe.get_medical_transcription_job(MedicalTranscriptionJobName=job_name)
    if status['MedicalTranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

The following example code shows the transcription results of a transcription job with speaker identification enabled\.

```
{
    "jobName": "job ID",
    "accountId": "account ID",
    "results": {
        "transcripts": [
            {
                "transcript": "Professional answer."
            }
        ],
        "speaker_labels": {
            "speakers": 1,
            "segments": [
                {
                    "start_time": "0.000000",
                    "speaker_label": "spk_0",
                    "end_time": "1.430",
                    "items": [
                        {
                            "start_time": "0.100",
                            "speaker_label": "spk_0",
                            "end_time": "0.690"
                        },
                        {
                            "start_time": "0.690",
                            "speaker_label": "spk_0",
                            "end_time": "1.210"
                        }
                    ]
                }
            ]
        },
        "items": [
            {
                "start_time": "0.100",
                "end_time": "0.690",
                "alternatives": [
                    {
                        "confidence": "0.8162",
                        "content": "Professional"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "0.690",
                "end_time": "1.210",
                "alternatives": [
                    {
                        "confidence": "0.9939",
                        "content": "answer"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "alternatives": [
                    {
                        "content": "."
                    }
                ],
                "type": "punctuation"
            }
        ]
    },
    "status": "COMPLETED"
}
```

## AWS CLI<a name="diarization-batch-cli"></a>

**To transcribe an audio file of a conversation between a clinician practicing primary care and a patient in an audio file and identify what each person said in the transcription output \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-transcription-job \
  –-cli-input-json file://example-start-command.json
  ```

  The following code shows the contents of `example-start-command.json`\.

  ```
  {
      "MedicalTranscriptionJobName": "speaker-id-conversation-medical-transcription-job",
      "LanguageCode": "language-code",
      "Specialty": "PRIMARYCARE",
      "Type": "CONVERSATION",
      "OutputBucketName":"DOC-EXAMPLE-BUCKET",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file.extension"
          },
      "Settings":{
          "ShowSpeakerLabels": true,
          "MaxSpeakerLabels": 2
          }
  }
  ```

  The following is the response from running the preceding CLI command\.

  ```
  {
      "MedicalTranscriptionJobName": "speaker-id-conversation-medical-transcription-job",
      "LanguageCode": "en-US",
      "Specialty": "PRIMARYCARE",
      "Type": "CONVERSATION",
      "OutputBucketName":"DOC-EXAMPLE-BUCKET1",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET1/example-file.extension"
          },
      "Settings":{
          "ShowSpeakerLabels": true,
          "MaxSpeakerLabels": 2
          }
  }
  ```