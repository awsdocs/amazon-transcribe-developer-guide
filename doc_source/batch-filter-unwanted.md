# Filtering batch transcriptions<a name="batch-filter-unwanted"></a>

Use a vocabulary filter to filter unwanted words from a batch transcription job with either the Amazon Transcribe console or the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\.

The following operation shows the parameters and data types\.

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

## Console<a name="batch-filter-console"></a>

To use the console to start a batch transcription job with vocabulary filtering, you must have created a vocabulary filter, as described in [Step 2: Creating a vocabulary filter](create-filter.md)\.

 **To filter unwanted words in a transcription job \(console\)** 

1. Sign in to AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. For **Name**, specify a name that is unique within your AWS account for your batch transcription job\.

1. For **Language**, choose the language that will be spoken in your transcription job\.

1. Specify the location of your audio file or video file in Amazon S3:
   + For **Input file location on S3** under **Input data**, specify the Amazon S3 URI that identifies the media file that you will transcribe\.
   + Choose **Browse S3** under **Input data** to browse for the media file and choose it\.

1. Choose **Next**\.

1. Enable **Vocabulary filtering** under **Content removal**\.

1. Choose your vocabulary filter and vocabulary filtering method under **Filter selection**\.

1. Choose **Create**\.

## API<a name="batch-filter-api"></a>

**To filter a batch transcription \(API\)**
+  In the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation, specify the following:

  1. For `TranscriptionJobName`, specify a name unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your media file and the language of your vocabulary filter\.

  1. In the `MediaFileUri` parameter of the `Media` object, specify the name of the media file that you want to transcribe\.

  1. For the `VocabularyFilterName` parameter, specify the name of your vocabulary filter\.

  1. For the `VocabularyFilterMethod` parameter, choose one of the following options:
     + To mask filtered words by replacing them with three asterisks `***`, specify `mask`\. Filtering the word "lazy" from the sentence: "The quick brown fox jumps over the lazy dog\." with the `mask` method shows "The quick brown fox jumps over the \*\*\* dog\." in the transcription\.
     + To remove the filtered words from the transcript, specify `remove`\. Filtering the word "lazy" from the sentence "The quick brown fox jumps over the lazy dog\." with the `remove` method shows "The quick brown fox jumps over the dog\." in the transcript\. 