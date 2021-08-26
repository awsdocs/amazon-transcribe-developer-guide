# Step 1: Creating a list of unwanted words<a name="create-filter-file"></a>

To create a vocabulary filter, you can create a list of words to filter from your transcription results and save them in a text file\. Or, you can use the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) API and enter the words that you want to filter as an array of strings in the `Words` parameter\. Although listing unwanted words in the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) API is more convenient, if you use a text file, you can edit your word list later and reuse it in another vocabulary filter\. 

The following guidelines apply to vocabulary filters:
+ Words in a vocabulary filter aren't case sensitive\. For example, "curse" and "CURSE" are considered the same word\.
+ Amazon Transcribe filters only words that exactly match words in the filter\. For example, if your filter includes "swear," Amazon Transcribe filters "swear," but not "swears\." You must provide every variation of a word that you want to filter\.
+  Amazon Transcribe doesn't filter words that are contained in other words\. For example, if a vocabulary filter contained "marine," but not "submarine," "submarine" would appear in your transcription results\. 

To create a word list with the console, complete the following procedure\. To use the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) API, see [Step 2: Creating a vocabulary filter](create-filter.md)\.

**To create a list of unfiltered words \(console\)**

1. In a text editor, create a new file and enter each word on a separate line followed by the newline \(\\n\) as shown in the following example\.

   ```
   profanity
   curse
   swear
   ...
   obscenity
   ```

1. Save the list as a plain text file locally or in Amazon Simple Storage Service \(Amazon S3\)\. 

**Next step**  
[Step 2: Creating a vocabulary filter](create-filter.md)