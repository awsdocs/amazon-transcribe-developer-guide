# Vocabulary Filtering<a name="how-vocabulary-filter"></a>

While transcribing a job, Amazon Transcribe can check the transcript for particular words, such as profane words, that you don't want in the transcript\. During transcription Amazon Transcribe filters these words from the transcript\. You can choose to remove words entirely or you can choose to replace the filtered words with placeholder text\.

To omit or redact specific words from the transcript, create a collection of words that Amazon Transcribe filters from the transcript\. You specify the list of words in a text file that you store in an S3 bucket or provide a list of words using the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) operation\. The following is an example of a list of words to filter from the transcript\.

```
word1
word2
word3
...
wordn
```

Each line contains a single word and ends with a newline \(\\n\) character\. The words are not case sensitive, "word1" and "WORD1" are considered the same word\.

To use a filter when you are transcribing an audio file, specify the name of the filter to use when you create the job with either the console or the API\. The output of the transcription is modified to remove the filtered words\. You can choose to mask the word, or you can completely remove the word from the transcript\. If you choose to mask words Amazon Transcribe replaces the word with three asterisks \("\*\*\*"\)\.

For example, consider the transcription of the sentence "I said, I don't like word1\!" If you choose to mask words, the output is 

```
I said, I don't like ***!
```

If you choose to remove words, the output is

```
I said, I don't like!
```

Amazon Transcribe does not filter words that appear inside other words\. For example, the word "upword1" is not filtered, nor is "up\-word1\." 

You create a filter by using the console or by using the Amazon Transcribe API\. For both, you provide a list of words to remove from the transcription\.

 To use the API, call the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) operation and either pass it the name of the filter and the S3 bucket location where the input file is stored, or pass it the name of the filter and a list of words to add\. Use the [GetVocabularyFilter](API_GetVocabularyFilter.md) to monitor the progress of creating the filter\.

To use the console, choose **Vocabulary filtering** and then choose **Create vocabulary filter**\. Give the filter a name and choose the source of words for the filter\. When you use the console you can either store the text file for the filter in an S3 bucket or you can upload the file from your local computer\. Choose **Create** to create the collection\. You can monitor the creation progress of the collection using the vocabulary filters list\.

You can manage your vocabulary filter using the console or the API\. You can use both to list the vocabulary filters in your account, get details of individual filters, and delete filters from your account\.