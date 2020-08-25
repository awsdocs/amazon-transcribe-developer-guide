# Identifying Speakers in Audio Files<a name="diarization-batch-med"></a>

You can enable speaker identification in a batch transcription job using either the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation or the Amazon Transcribe Medical console\.

The following syntax shows the request parameters and their data types\. 

## Console<a name="diarization-batch-med-console"></a>

**To enable speaker identification in a transcription job \(console\)**

To use the console to enable speaker identification in your transcription job, you enable audio identification and then speaker identification\.

1. Sign in to AWS Management Console and open the Amazon Transcribe Medical console at [Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Audio identification**\.

1. For **Audio identification type**, choose **Speaker identification**\.

1. For **Maximum number of speakers**, enter the maximum number of speakers that you think are speaking in your audio file\. For best results, match the number of speakers that you ask to identify to the number of speakers in the input audio\. If you specify a value less than the number of speakers in your input audio, the transcription text of the most similar sounding speakers are attributed to a speaker label\. 

1. Choose **Create**\.

## API<a name="diarization-batch-med-api"></a>

**To identify speakers in an audio file using a batch transcription job \(API\)**
+  In the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation, specify the following\.

  1. For `TranscriptionJobName`, specify a name unique in your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file and the language of your vocabulary filter\.

  1. In the `MediaFileUri` parameter of the `Media` object, specify the name of the audio file that you want to transcribe\.

  1. For the `Settings` object, specify the following\.

     1. `ShowSpeakerLabels` – `true`\.

     1. `MaxSpeakerLabels` \- An integer between 2 and 10 to indicate the number of speakers that you think are speaking in your audio\. For best results, match the number of speakers that you ask to identify to the number of speakers in the input audio\. If you specify a value less than the number of speakers in your input audio, the transcription text of the most similar sounding speakers are attributed to the same speaker label\. 

The following shows the request parameters to start a batch transcription job and their data types\.

```
{
    "LanguageCode": "string",
    "Media": {
        "MediaFileUri": "string"
    },
    "MediaFormat": "string",
    "MediaSampleRateHertz": number,
    "MedicalTranscriptionJobName": "string",
    "OutputBucketName": "string",
    "OutputEncryptionKMSKeyId": "string",
    "Settings": {
        "ChannelIdentification": boolean,
        "MaxAlternatives": number,
        "MaxSpeakerLabels": number,
        "ShowAlternatives": boolean,
        "ShowSpeakerLabels": boolean,
        "VocabularyName": "string"
    },
    "Specialty": "string",
    "Type": "string"
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