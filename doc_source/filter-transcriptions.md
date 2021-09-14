# Step 3: Filtering transcriptions<a name="filter-transcriptions"></a>

You can filter unwanted words from both batch and streaming transcriptions\. When you create a real\-time stream or batch transcription job, specify the vocabulary filter that you want to use and the vocabulary filter method\. The method specifies how the words are filtered from your transcription results\. There are two vocabulary filter methods available for batch transcription and three methods available for real\-time streaming\.

You can use the following filter methods for both batch and real\-time streaming transcriptions:
+ To replace the words caught by your vocabulary filter with three asterisks, `***`, use the `mask` method\. Use this method to hide unwanted words from your audience, but indicate that they were spoken\.
+ To remove the words from your transcripts, use the `remove` method\. With this method, your audience won't know that unwanted words were spoken\.

In real\-time streaming transcriptions *only*, you can use the `tag` method to keep unwanted words in your transcription results with a tag that indicates that they were listed in your vocabulary filter\. You can then manually remove the words from some transcripts and leave them in others to generate transcripts for multiple audiences from a single stream\.

For information about streaming transcriptions, see [Transcribing streaming audio](streaming.md)\. For information about batch transcriptions, see [How Amazon Transcribe works](how-it-works.md)\.

**Topics**
+ [Filtering batch transcriptions](batch-filter-unwanted.md)
+ [Filtering streaming transcriptions](streaming-filter-unwanted.md)