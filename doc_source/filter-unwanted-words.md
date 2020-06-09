# Use Vocabulary Filtering to Filter Unwanted Words<a name="filter-unwanted-words"></a>

You can mask or remove words that you don't want to appear in your transcription results with *vocabulary filtering*\. For example, you can use vocabulary filtering to prevent the display of offensive or profane terms\. This enables you to generate family\-friendly captions of a TV show or transcripts of conferences that are appropriate for your audiences\. Use vocabulary filtering for any word that you consider profane, obscene, offensive, or otherwise unsuitable for the readers of your transcripts\. 

Vocabulary filtering is available for both real\-time streaming and batch processing\. For both transcription processing methods, you can either mask unwanted words \(replace them with three asterisks \(\*\*\*\) in your transcription\) or remove them completely\. For real\-time streaming *only*, you can use tags to mark words that are listed in your vocabulary filter in your transcription results\. You can then manually remove the words from some transcripts and leave them in others to generate transcripts for multiple audiences from a single stream\. 

To filter unwanted words, you:

1. Create a list of unwanted words\.

1. Create a vocabulary filter\.

1. Start your real\-time stream or transcription job and specify your vocabulary filter and method\. The method \(mask, remove, or tag\) indicates how you want to filter words from your transcript\.

You can filter unwanted words with the Amazon Transcribe console or the API\. 

**Topics**
+ [Step 1: Creating a List of Unwanted Words](create-filter-file.md)
+ [Step 2: Creating a Vocabulary Filter](create-filter.md)
+ [Step 3: Filtering Transcriptions](filter-transcriptions.md)