# Step 2: Creating a vocabulary filter<a name="create-filter"></a>

You can create a vocabulary filter with either the [CreateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabularyFilter.html) API or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

If you use the [CreateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabularyFilter.html) API, you can enter the words in your vocabulary filter as an array of strings into the `Words` parameter\. Although this method is more convenient, if you create a text file, you can edit your word list later and reuse it in another vocabulary filter\. 

## AWS Management Console<a name="create-filter-console"></a>

****

To use the AWS Management Console to create a vocabulary filter, you must have a plain text file that contains the words that you want to filter, formatted as described in [Step 1: Creating a list of unwanted words ](create-filter-file.md)\. Your file can be saved locally or in Amazon Simple Storage Service \(Amazon S3\)\. 

**To create a vocabulary filter \(AWS Management Console\)**

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

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
+ For the [CreateVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabularyFilter.html) API, specify the following:

  1. A name for your vocabulary filter that is unique in your AWS account for the `VocabularyFilterName` parameter

  1. The language code for the language of your source audio in the `LanguageCode` parameter

  1. The words for your vocabulary filter using one of the following options:
     + Specify the Amazon Simple Storage Service \(Amazon S3\) location of the text file for the `VocabularyFilterFileUri` parameter using this format: `s3://DOC-EXAMPLE-BUCKET/my-vocabulary-filter.txt`\.
     + Enter the words as an array of strings in the `Words` parameter, for example `["word", "banana", "potato", "chair"]`\.

To see all of the vocabulary filters that you've created, use the [ListVocabularyFilters](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularyFilters.html) API\. You can then use that information with the [GetVocabularyFilter](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabularyFilter.html) API to retrieve the download URI for your vocabulary filter and learn more about that filter\.

## AWS CLI<a name="create-filter-cli"></a>

The following is an example AWS Command Line Interface \(AWS CLI\) request to create a vocabulary filter with a text file stored in an Amazon S3 bucket\. The commands are followed by the response elements in JSON format\.

```
aws transcribe create-vocabulary-filter \ 
    --vocabulary-filter-name my-first-vocabulary-filter  \ 
    --language-code en-US \ 
    --vocabulary-filter-file-uri s3://DOC-EXAMPLE-BUCKET/vocabulary-filter-example.txt
                    
                    
{                  
    "VocabularyFilterName": "my-first-vocabulary-filter",
    "LanguageCode": "en-US"
}
```

**Next step**  
[Step 3: Filtering transcriptions](filter-transcriptions.md)