# Using vocabulary filtering to filter unwanted words<a name="vocabulary-filtering"></a>

You can mask, remove, or tag words you don't want in your transcription results with *vocabulary filtering*\. For example, you can use vocabulary filtering to prevent the display of offensive or profane terms\.

You can use the following methods to filter unwanted words from your transcription results:
+ Mask: replace unwanted words with three asterisks \(\*\*\*\)
+ Remove: remove the unwanted words
+ Tag: mark words that are listed in your vocabulary filter in the transcription results

You can use tagging to manually remove the words from some transcripts and leave them in others\. This enables you to generate transcripts for multiple audiences from a single stream\.

To filter unwanted words, you:

1. Create a list of unwanted words\.

1. Create a vocabulary filter\.

1. Start your real\-time stream or transcription job and specify your vocabulary filter and method\. The method \(mask, remove, or tag\) indicates how you want to filter words from your transcript\.

You can filter unwanted words with the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/) or the API\. 

**Topics**
+ [Step 1: Creating a list of unwanted words](create-filter-file.md)
+ [Step 2: Creating a vocabulary filter](create-filter.md)
+ [Step 3: Filtering transcriptions](filter-transcriptions.md)