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

1. Start your real\-time stream or transcription job and specify your vocabulary filter and method\. The method \(mask, remove, or tag\) indicates how you want your transcription output to display filtered words in your transcript\.

**API operations specific to vocabulary filtering**  
 [CreateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/dg/API_CreateVocabularyFilter.html), [DeleteVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/dg/API_DeleteVocabularyFilter.html), [GetVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/dg/API_GetVocabularyFilter.html), [ListVocabularyFilters](https://docs.aws.amazon.com/transcribe/latest/dg/API_ListVocabularyFilters.html), [UpdateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/dg/API_UpdateVocabularyFilter.html) 