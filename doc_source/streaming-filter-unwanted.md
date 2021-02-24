# Filtering streaming transcriptions<a name="streaming-filter-unwanted"></a>

Use a vocabulary filter to filter unwanted words in real\-time streams with either the Amazon Transcribe console or the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation\. 

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
+ In the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation, specify the following:

  1. The language code of your audio in the `LanguageCode` field\.

  1. The sample rate of your audio in the `MediaSampleHertz` field\.

  1. The name of your vocabulary filter in the `VocabularyFilterName` field\.

  1. The filtering method in the `VocabularyFilterMethod` parameter: 
     + To mask the filtered words by replacing them with three asterisks \(`***`\) specify `mask`\. Filtering the word "lazy" from the sentence "The quick brown fox jumps over the lazy dog\." with the `mask` method shows "The quick brown fox jumps over the \*\*\* dog\." in the transcription\. 
     + To remove the words from the transcript, specify `remove`\. Filtering the word "lazy" from the sentence "The quick brown fox jumps over the lazy dog\." with the `remove` method shows "The quick brown fox jumps over the dog\." in the transcription\.

To use the same stream to create one transcript with the content filtered and one transcript that is unfiltered, use the tagging method\. For information, see [Tailoring transcripts to different audiences with tagging](#filter-two-transcripts)\.

**To filter a streaming transcription \(console\)**

1. Sign into the AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. In **Language**, choose the language of your real\-time stream\.

1. Choose the **Additional settings** tab and choose your vocabulary filter and vocabulary filtering method\.

1. Choose **Start streaming** to begin your stream with vocabulary filtering enabled\.

## Tailoring transcripts to different audiences with tagging<a name="filter-two-transcripts"></a>

You can use a single stream to generate a transcription that doesn't show unwanted words and one that does\. In the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation, use the `tag` method to mark the words in the transcription that match the words in your vocabulary filter\. You can present the results of the real\-time stream to the audience that can see the complete transcription, including the words listed in your vocabulary filter\. You can then copy your transcription results, remove the words tagged by your vocabulary filter, and show those results to the audience that shouldn't see the unwanted words\. 

With tagging, you aren't limited to generating transcriptions for two different audiences\. You can generate multiple transcriptions for many audiences from the same stream\. You can choose to remove some words caught by the vocabulary filter in one transcript and leave them in other transcripts\.

**To enable tagging in a real\-time transcription**
+ In the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation, specify the following:

  1. For `VocabularyFilterName`, the name of your vocabulary filter\.

  1. For `VocabularyFilterMethod`, specify `tag`\.

  For example, if "lazy" were in the vocabulary filter, the sentence "The quick brown fox jumps over the lazy dog\." would be unchanged in the transcription results\. Instead of being masked in, or removed from, the transcription, the value for the `VocabularyFilterMatch` parameter would be `true` for "lazy\." 

The following example JSON output shows this\.

```
                        "Transcript": {
            "Results": [
                {
                ...
                    "Alternatives": [
                        {
                            "Items": [
                            ...
                                {
                                    "Content": "jumps",
                                    "EndTime": 1.02,
                                    "StartTime": 0.98,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": false
                                },
                                {
                                    "Content": "over",
                                    "EndTime": 1.26,
                                    "StartTime": 1.03,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": false
                                },
                                {
                                    "Content": "the",
                                    "EndTime": 1.41,
                                    "StartTime": 1.27,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": false
                                },
                                {
                                    "Content": "lazy",
                                    "EndTime": 1.81,
                                    "StartTime": 1.42,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": true
                                }
                                ...
                                ]
                                }
                                    ]
                                        }
                                           ]
                                               }
```