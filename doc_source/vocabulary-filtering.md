# Using vocabulary filtering with unwanted words<a name="vocabulary-filtering"></a>

Mask, remove, or tag words you don't want in your transcription results using *vocabulary filtering*\.

A common use case is the removal of offensive or profane terms from your transcripts; however, vocabulary filters are completely custom, so you can select any words\. For example, if you have a new product about to launch, you can mask the product name in meeting transcripts\. In this case, you keep stakeholders up\-to\-date while still keeping the product name secret until launch\.

Vocabulary filtering has three different display options:
+ **Masked content** — Replaces unwanted words with three asterisks \(\*\*\*\)\.
+ **Content removal** — Content removal: Deletes unwanted words, leaving nothing in their place\.
+ **Tags** — Adds a tag to each word in your transcription output that matches a words in your vocabulary filter\. Tagging is typically used when you want to remove words from select transcripts\. For example, if you're creating subtitles for a movie, you may want to leave profanity in for adult screenings, but remove it for family\-friendly screenings\.

To filter unwanted words, you:

1. Create a list of unwanted words\.

1. Create a vocabulary filter\.

1. Start your real\-time stream or transcription job and specify your vocabulary filter and method\. The method \(mask, remove, or tag\) indicates how you want your transcription output to display filtered words in your transcript\.

**API operations specific to vocabulary filtering**  
 [CreateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabularyFilter.html), [DeleteVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteVocabularyFilter.html), [GetVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabularyFilter.html), [ListVocabularyFilters](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularyFilters.html), [UpdateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateVocabularyFilter.html) 

For a video walkthrough of vocabulary filtering, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/TcpSqbr0FnI/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/TcpSqbr0FnI)

To dive a little deeper and learn how to use Amazon Augmented AI with custom vocabularies, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/65eVesNiJzY/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/65eVesNiJzY)