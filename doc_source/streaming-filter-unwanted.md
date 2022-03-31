# Filtering streaming transcriptions<a name="streaming-filter-unwanted"></a>

Use a vocabulary filter to filter unwanted words in real\-time streams with either the [AWS Management Console](https://console.aws.amazon.com/transcribe/) or the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API\.

The following syntax shows the parameters and their data types\.

```
{
    "LanguageCode" : "enum",
    "MediaSampleRateHertz" : "integer",
    "MediaEncoding" : "enum",
    "VocabularyName" : "string",
    "SessionId" : "string", 
    "AudioStream" : "eventstream",
    "VocabularyFilterName" : "string",
    "VocabularyFilterMethod": "enum"
}
```

**To filter a streaming transcription \(API\)**
+ For the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API, specify the following:

  1. The language code of your audio in the `LanguageCode` field\.

  1. The sample rate of your audio in the `MediaSampleHertz` field\.

  1. The name of your vocabulary filter in the `VocabularyFilterName` field\.

  1. The filtering method in the `VocabularyFilterMethod` parameter: 
     + To mask the filtered words by replacing them with three asterisks \(`***`\) specify `mask`\. Filtering the word "lazy" from the sentence "The quick brown fox jumps over the lazy dog\." with the `mask` method shows "The quick brown fox jumps over the \*\*\* dog\." in the transcription\. 
     + To remove the words from the transcript, specify `remove`\. Filtering the word "lazy" from the sentence "The quick brown fox jumps over the lazy dog\." with the `remove` method shows "The quick brown fox jumps over the dog\." in the transcription\.
     + To tag words that match the vocabulary filter, specify `tag`\. This enables you

        to mark the words matching the vocabulary filter without masking or removing them\.

To use the same stream to create one transcript with the content filtered and one transcript that is unfiltered, use the tagging method\. For information, see [Tailoring transcripts to different audiences with tagging](#filter-two-transcripts)\.

**To filter a streaming transcription \(AWS Management Console\)**

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. In **Language**, choose the language of your real\-time stream\.

1. Choose the **Additional settings** tab and choose your vocabulary filter and vocabulary filtering method\.

1. Choose **Start streaming** to begin your stream with vocabulary filtering enabled\.

## Tailoring transcripts to different audiences with tagging<a name="filter-two-transcripts"></a>

You can use a single stream to generate a transcription that doesn't show unwanted words and one that does\. For the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API, use the `tag` method to mark the words in the transcription that match the words in your vocabulary filter\. You can present the results of the real\-time stream to the audience that can see the complete transcription, including the words listed in your vocabulary filter\. You can then copy your transcription results, remove the words tagged by your vocabulary filter, and show those results to the audience that shouldn't see the unwanted words\. 

With tagging, you aren't limited to generating transcriptions for two different audiences\. You can generate multiple transcriptions for many audiences from the same stream\. You can choose to remove some words caught by the vocabulary filter in one transcript and leave them in other transcripts\.

**To enable tagging in a real\-time transcription**
+ For the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API, specify the following:

  1. For `VocabularyFilterName`, the name of your vocabulary filter\.

  1. For `VocabularyFilterMethod`, specify `tag`\.

  For example, if "bloody" were in the vocabulary filter, the phrase "recording bloody well set up this stupid bloody meeting anyway\.\.\." would be unchanged in the transcription results\. Instead of being masked in, or removed from, the transcription, the value for the `VocabularyFilterMatch` parameter would be `true` for "bloody\." 

The following example JSON output shows this\.

```
   {
    "jobName": "my-first-transcription-job",
    "accountId": "111122223333",
    "results": {
        "transcripts": [
            {
                "transcript": "...recording bloody well set up this stupid bloody meeting anyway..."
            }
        ],
        "items": [
            {
                "start_time": "5.4",
                "end_time": "5.95",
                "alternatives": [
                    {
                        "confidence": "0.9966",
                        "content": "recording"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            },
            {
                "start_time": "7.84",
                "end_time": "8.54",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "bloody"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": true
            },
            {
                "start_time": "8.54",
                "end_time": "9.03",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "well"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            },
            {
                "start_time": "9.04",
                "end_time": "9.31",
                "alternatives": [
                    {
                        "confidence": "0.9905",
                        "content": "set"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            },
            {
                "start_time": "9.31",
                "end_time": "9.44",
                "alternatives": [
                    {
                        "confidence": "0.9905",
                        "content": "up"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            },
            {
                "start_time": "9.44",
                "end_time": "9.6",
                "alternatives": [
                    {
                        "confidence": "0.8796",
                        "content": "this"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            },
            {
                "start_time": "9.6",
                "end_time": "10.22",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "stupid"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            },
            {
                "start_time": "10.23",
                "end_time": "10.66",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "bloody"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": true
            },
            {
                "start_time": "10.66",
                "end_time": "11.21",
                "alternatives": [
                    {
                        "confidence": "0.9994",
                        "content": "meeting"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            },
            {
                "start_time": "11.21",
                "end_time": "11.55",
                "alternatives": [
                    {
                        "confidence": "0.9978",
                        "content": "anyway"
                    }
                ],
                "type": "pronunciation",
                "vocabularyFilterMatch": false
            }
        ]
    },
    "status": "COMPLETED"
}
```