# Filtering batch transcriptions<a name="batch-filter-unwanted"></a>

Use a vocabulary filter to filter unwanted words from a batch transcription job with either the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/) or the [StartTranscriptionJob](API_StartTranscriptionJob.md) API\.

The following code shows the parameters and data types\.

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

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. For **Name**, specify a name that is unique within your AWS account for your batch transcription job\.

1. For **Language**, choose the language that will be spoken in your transcription job\.

1. Specify the location of your audio file or video file in Amazon S3:
   + For **Input file location on S3** under **Input data**, specify the Amazon S3 URI that identifies the media file that you will transcribe\.

     1. Choose **Browse S3** under **Input data** to browse for the media file and choose it\.

1. Choose **Next**\.

1. Enable **Vocabulary filtering** under **Content removal**\.

1. Choose your vocabulary filter and vocabulary filtering method under **Filter selection**\.

1. Choose **Create**\.

## API<a name="batch-filter-api"></a>

**To filter a batch transcription \(API\)**
+ For the [StartTranscriptionJob](API_StartTranscriptionJob.md) API, specify the following:

  1. For `TranscriptionJobName`, specify a name unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your media file and the language of your vocabulary filter\.

  1. For the `MediaFileUri` parameter of the `Media` object, specify the Amazon S3 location of the audio file or video file that you want to transcribe\.

  1. For the `VocabularyFilterName` parameter, specify the name of your vocabulary filter\.

  1. For the `VocabularyFilterMethod` parameter, choose one of the following options:
     + To mask filtered words by replacing them with three asterisks `***`, specify `mask`\. Filtering the word "lazy" from the sentence: "The quick brown fox jumps over the lazy dog\." with the `mask` method shows "The quick brown fox jumps over the \*\*\* dog\." in the transcription\.
     + To remove the filtered words from the transcript, specify `remove`\. Filtering the word "lazy" from the sentence "The quick brown fox jumps over the lazy dog\." with the `remove` method shows "The quick brown fox jumps over the dog\." in the transcript\. 
     + To mark words that match your vocabulary filter in the transcript, specify `tag`\. Use this to produce transcripts that are tailored to different audiences\. This enables you to: 
       + Present the transcription results to one audience, without removing any of the marked words that match the vocabulary filter\.
       + Remove any word that matched the vocabulary filter, and present those results to a different audience\.
       + Remove some words that matched the vocabulary filter, and present those results to a another audience\. You can generate multiple transcriptions for many audiences from the same transcription output\. For more information, see [Tailoring transcripts to different audiences with tagging](#batch-tailor-transcripts)\. 

## Tailoring transcripts to different audiences with tagging<a name="batch-tailor-transcripts"></a>

You can generate multiple transcriptions tailored to different audiences from a single audio file\. For the [StartTranscriptionJob](API_StartTranscriptionJob.md) API, use the `tag` method to mark the words in the transcription that match the words in your vocabulary filter\. You can present the results of the transcription job to the audience that can see the complete transcription, including the words listed in your vocabulary filter\. You can then copy your transcription results, remove the words tagged by your vocabulary filter, and show those results to the audience that shouldn't see the unwanted words\. 

With tagging, you aren't limited to generating transcriptions for two different audiences\. You can generate multiple transcriptions for many audiences from the same audio file\. You can choose to remove some words caught by the vocabulary filter in one transcript and leave them in other transcripts\.

For example, if "lazy" were in the vocabulary filter, the sentence "The quick brown fox jumps over the lazy dog\." would be unchanged in the transcription results\. Instead of being masked in, or removed from, the transcription, the value for the `VocabularyFilterMatch` parameter would be `true` for "lazy\." 

To enable tagging in your batch transcription job, see [Filtering batch transcriptions](#batch-filter-unwanted)\.

The word "bloody" is tagged in the following truncated transcription output\.

```
{
   "jobName":"transcription-job-name",
   "accountId":"account-id",
   "results":{
      "transcripts":[
         {
            "transcript":"...recording bloody well set up this stupid bloody meeting anyway..."
                ... }
                            "items": [
                            ...
                                         {
            "start_time":"5.4",
            "end_time":"5.95",
            "alternatives":[
               {
                  "confidence":"0.9966",
                  "content":"recording"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         },
         {
            "start_time":"7.84",
            "end_time":"8.54",
            "alternatives":[
               {
                  "confidence":"1.0",
                  "content":"bloody"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":true
         },
         {
            "start_time":"8.54",
            "end_time":"9.03",
            "alternatives":[
               {
                  "confidence":"1.0",
                  "content":"well"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         },
         {
            "start_time":"9.04",
            "end_time":"9.31",
            "alternatives":[
               {
                  "confidence":"0.9905",
                  "content":"set"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         },
         {
            "start_time":"9.31",
            "end_time":"9.44",
            "alternatives":[
               {
                  "confidence":"0.9905",
                  "content":"up"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         },
         {
            "start_time":"9.44",
            "end_time":"9.6",
            "alternatives":[
               {
                  "confidence":"0.8796",
                  "content":"this"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         },
         {
            "start_time":"9.6",
            "end_time":"10.22",
            "alternatives":[
               {
                  "confidence":"1.0",
                  "content":"stupid"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         },
         {
            "start_time":"10.23",
            "end_time":"10.66",
            "alternatives":[
               {
                  "confidence":"1.0",
                  "content":"bloody"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":true
         },
         {
            "start_time":"10.66",
            "end_time":"11.21",
            "alternatives":[
               {
                  "confidence":"0.9994",
                  "content":"meeting"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         },
         {
            "start_time":"11.21",
            "end_time":"11.55",
            "alternatives":[
               {
                  "confidence":"0.9978",
                  "content":"anyway"
               }
            ],
            "type":"pronunciation",
            "vocabularyFilterMatch":false
         }
                                ...
                                ]
                                },
         "status":"COMPLETED"
                                        }
```