# Step 2: Creating a Vocabulary Filter<a name="create-filter"></a>

You can create a vocabulary filter with either the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) operation or the Amazon Transcribe console\.

If you use the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) operation, you can enter the words in your vocabulary filter as an array of strings into the `Words` parameter\. Although this method is more convenient, if you create a text file, you can edit your word list later and reuse it in another vocabulary filter\. 

## Console<a name="create-filter-console"></a>

**Creating a Vocabulary Filter \(Console\)**

To use the console to create a vocabulary filter, you must have a plain text file that contains the words that you want to filter, formatted as described in [Step 1: Creating a List of Unwanted Words ](create-filter-file.md)\. Your file can be saved locally or in Amazon Simple Storage Service \(Amazon S3\)\. 

**To create a vocabulary filter \(console\)**

1. Sign in to AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Vocabulary filtering**\.

1. Choose **Create vocabulary filter**\.

1. For **Name**, enter a vocabulary filter name that is unique within your AWS account\.

1. For **Language**, choose the language code for the language of your vocabulary filter\. 

1. For **Vocabulary input source**, choose one of the following:
   + If you saved the file that contains the word that you want to filter locally, choose **File upload**, then choose **Choose file** and choose the file\. 
   + If you saved the file in Amazon S3, for **S3 location**, enter the URI of the text file or choose **Browse S3** and browse to the file and choose it\.

1. Choose **Create vocabulary filter**\.

## API<a name="create-filter-api"></a>

**To create a vocabulary filter \(API\)**
+ In the [CreateVocabularyFilter](API_CreateVocabularyFilter.md) operation, specify the following:

  1. A name for your vocabulary filter that is unique in your AWS account for the `VocabularyFilterName` parameter

  1. The language code for the language of your source audio in the `LanguageCode` parameter

  1. The words for your vocabulary filter using one of the following options:
     + Specify the Amazon Simple Storage Service \(Amazon S3\) location of the text file in the `VocabularyFilterFileUri` parameter using this format: `s3://DOC-EXAMPLE-BUCKET1/vocabulary-filter-example.txt`\.
     + Enter the words as an array of strings in the `Words` parameter, for example `["word", "banana", "potato", "chair"]`\.

To see all of the vocabulary filters that you've created, use the [ListVocabularyFilters](API_ListVocabularyFilters.md) operation\. You can then use that information with the [GetVocabularyFilter](API_GetVocabularyFilter.md) operation to retrieve the download URI for your vocabulary filter and learn more about that filter\.

## AWS CLI<a name="create-filter-cli"></a>

The following is an example AWS Command Line Interface \(AWS CLI\) request to create a vocabulary filter with a text file stored in an Amazon S3 bucket\. The commands are followed by the response elements in JSON format\.

```
aws transcribe create-vocabulary-filter \ 
    --vocabulary-filter-name your-filter-name  \ 
    --language-code en-US \ 
    --vocabulary-filter-file-uri s3://DOC-EXAMPLE-BUCKET1/vocabulary-filter-example.txt
                    
                    
{                  
    "VocabularyFilterName": "your-filter-name",
    "LanguageCode": "en-US"
}
```

**Next Step**  
[Step 3: Filtering Transcriptions](filter-transcriptions.md)