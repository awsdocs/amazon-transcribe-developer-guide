# Using custom vocabulary filters to delete, mask, or flag words<a name="vocabulary-filtering"></a>

A custom vocabulary filter is a text file that contains a custom list of individual words that you want to modify in your transcription output\.

A common use case is the removal of offensive or profane terms; however, custom vocabulary filters are completely custom, so you can select any words you want\. For example, if you have a new product about to launch, you can mask the product name in meeting transcripts\. In this case, you keep stakeholders up\-to\-date while keeping the product name secret until launch\.

Vocabulary filtering has three display methods: `mask`, `remove`, and `tag`\. Refer to the following examples to see how each works\.
+ **Mask**: Replaces specified words with three asterisks \(\*\*\*\)\.

  ```
  "transcript": "You can specify a list of *** or *** words, and *** *** removes them from transcripts automatically."
  ```
+ **Remove**: Deletes specified words, leaving nothing in their place\.

  ```
  "transcript": "You can specify a list of or words, and removes them from transcripts automatically."
  ```
+ **Tag**: Adds a tag \(`"vocabularyFilterMatch": true`\) to each specified word, but doesn't alter the word itself\. Tagging allows for rapid transcript substitutions and edits\.

  ```
  "transcript": "You can specify a list of profane or offensive words, and amazon transcribe removes them from transcripts automatically."
  ...
      "alternatives": [
          {
              "confidence": "1.0",
              "content": "profane"
          }
      ],
      "type": "pronunciation",
      "vocabularyFilterMatch": true
  ```

When you submit a transcription request, you can specify a custom vocabulary filter and the filtration method you want to apply\. Amazon Transcribe then modifies exact word matches when they appear in your transcript, according to the filtration method you specify\.

Custom vocabulary filters can be applied to batch and streaming transcription requests\. To learn how to create a custom vocabulary filter, see [Creating a vocabulary filter](vocabulary-filter-create.md)\. To learn how to apply your custom vocabulary filter, see [Using a custom vocabulary filter](vocabulary-filter-using.md)\.

For a video walkthrough of vocabulary filtering, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/TcpSqbr0FnI/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/TcpSqbr0FnI)

**API operations specific to vocabulary filtering**  
 [CreateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabularyFilter.html), [DeleteVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteVocabularyFilter.html), [GetVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabularyFilter.html), [ListVocabularyFilters](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularyFilters.html), [UpdateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateVocabularyFilter.html) 