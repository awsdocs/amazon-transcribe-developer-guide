# Identifying speakers in audio files<a name="diarization-batch"></a>

You can enable speaker diarization in a batch transcription job using either the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation or the Amazon Transcribe console\.

## Console<a name="diarization-batch-console"></a>

**To identify speakers in an audio file \(console\)**

To use the console to enable speaker diarization in your transcription job, you enable audio identification and then speaker diarization\.

1. Sign in to AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Audio identification**\.

1. For **Audio identification type**, choose **Speaker identification**\.

1. For **Maximum number of speakers**, specify the maximum number of speakers that you think are speaking in your audio\. For best results, match the number of speakers that you ask to identify to the number of speakers in the input audio\. If you specify a value less than the number of speakers in your input audio, the transcription text of the most similar sounding speakers are attributed to a speaker label\.

1. Choose **Create**\.

## API<a name="diarization-batch-api"></a>

**To identify speakers in an audio file using a batch transcription job \(API\)**
+  In the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation, specify the following\.

  1. For `TranscriptionJobName`, specify a name unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your media file and the language of your vocabulary filter\.

  1. In the `MediaFileUri` parameter of the `Media` object, specify the name of the media file that you want to transcribe\.

  1. For the `Settings` object, specify the following\.

     1. `ShowSpeakerLabels` – `true`\.

     1.  `MaxSpeakerLabels` \- An integer between 2 and 10 for that indicates the number of speakers that you think are speaking in your audio\. For best results, match the number of speakers that you ask to identify to the number of speakers in the input audio\. If you specify a value less than the number of speakers in your input audio, the transcription text of the most similar sounding speakers are attributed to a speaker label\. 

The following syntax shows the request parameters to start a batch transcription job and their data types\.

```
    {
       "ContentRedaction": { 
          "RedactionOutput": "string",
          "RedactionType": "string"
       },
       "JobExecutionSettings": { 
          "AllowDeferredExecution": boolean,
          "DataAccessRoleArn": "string"
       },
       "LanguageCode": "string",
       "Media": { 
          "MediaFileUri": "string"
       },
       "MediaFormat": "string",
       "MediaSampleRateHertz": number,
       "OutputBucketName": "string",
       "OutputEncryptionKMSKeyId": "string",
       "Settings": { 
          "ChannelIdentification": boolean,
          "MaxAlternatives": number,
          "MaxSpeakerLabels": number,
          "ShowAlternatives": boolean,
          "ShowSpeakerLabels": boolean,
          "VocabularyFilterMethod": "string",
          "VocabularyFilterName": "string",
          "VocabularyName": "string"
       },
       "TranscriptionJobName": "string"
    }
```

The following code shows an example output of a transcription job with speaker identification enabled\.

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

**To identify the speakers in an audio file using a batch transcription job \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-transcription-job \
  --cli-input-json file://example-start-command.json
  ```

  The following code shows the contents of `example-start-command.json`\.

  ```
    {
      "TranscriptionJobName": "your-transcription-job-name",
      "LanguageCode": "en-US",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file.mp4"
      },
      "Settings":{
          "MaxSpeakerLabels": 2,
    "ShowSpeakerLabels":true
    }
  ```

  The following is the response from running the preceding CLI command\.

  ```
  {
      "TranscriptionJob": {
          "TranscriptionJobName": "your-transcription-job-name",
          "TranscriptionJobStatus": "IN_PROGRESS",
          "LanguageCode": "en-US",
          "Media": {
              "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET1/your-audio-file"
          },
          "StartTime": "2020-07-29T17:45:09.826000+00:00",
          "CreationTime": "2020-07-29T17:45:09.791000+00:00",
          "Settings": {
              "ShowSpeakerLabels": true,
              "MaxSpeakerLabels": 2
        }
      }
  }
  ```