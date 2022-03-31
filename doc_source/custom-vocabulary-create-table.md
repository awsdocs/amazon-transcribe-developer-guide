# Creating a custom vocabulary using a table<a name="custom-vocabulary-create-table"></a>

Using a table format is the most robust way to create your custom vocabulary\. Vocabulary tables consist of four columns, and these columns can be in any order:


| Phrase | SoundsLike | IPA | DisplayAs | 
| --- | --- | --- | --- | 
|  Required\. Every row in your table must contain an entry in this column\. If your entry contains multiple words, separate each word with a hyphen \(\-\); do not use spaces\. For example, **Andorra\-la\-Vella** or **Los\-Angeles**\. For acronyms, any pronounced letters must be separated by a period\. If your acronym is plural, you must use a hyphen between the acronym and the 's'\. For example, 'CLI' is **C\.L\.I\.** and 'ABCs' is **A\.B\.C\.\-s**\. If your phrase consists of both a word and an acronym, these two components must be separated by a hyphen\. For example, 'DynamoDB' is **Dynamo\-D\.B\.**\. Do not use spaces in this column\.  |  Optional\. Rows in this column can be left empty\. Break your entry down into hyphen\-separated syllables that mimic how the word sounds\. For example, **Andorra\-la\-Vella** sounds like **ann\-dor\-ah\-la\-bey\-ah** and **Los\-Angeles** sounds like **loss\-ann\-gel\-es**\. Do not use spaces in this column\. If you have an entry in this column, your `IPA` column must be empty\.  |  Optional\. Rows in this column can be left empty\. This column is intended for phonetic spellings using only characters in the [International Phonetic Alphabet \(IPA\)](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet)\. For example, 'Los Angeles' is **l ɔ s æ n ʤ ə l ə s** and 'CLI' is **s ɪ ɛ l aɪ**\. You must add a single space between every IPA character \(single\-byte\) or valid IPA character pair \(double\-byte\)\. If you have an entry in this column, your `SoundsLike` column must be empty\.  |  Optional\. Rows in this column can be left empty\. Defines the how you want your entry to look in your transcription output\. For example, **Andorra\-la\-Vella** in the `Phrase` column is **Andorra la Vella** in the `DisplayAs` column\. If a row in this column is empty, Amazon Transcribe uses the contents of the `Phrase` column to determine output\. You can use spaces in this column\.  | 

Things to note when creating your table:
+ Your table must contain all four columns \(Phrase, SoundsLike, IPA, and DisplayAs\), but the `Phrase` column is the only one that must contain an entry on each row\. All other columns can be left empty\.
+ In a given row, you cannot have entries for both `IPA` and `SoundsLike` fields\. You must choose one or the other, or leave both blank\.
+ You can only use characters that are supported for your language\. Refer to your language's [character set](charsets.md) for details\.
+ Only use spaces *within* the `IPA` and `DisplayAs` columns\. Separate columns with a TAB character\. Do not use spaces to separate columns; doing so results in an error\.
+ Only add content in the `SoundsLike` column if your entry includes a non\-standard word, such as a brand name\.
+ You must save your table as a text \(\*\.txt\) file and upload it into an S3 bucket before you can convert it into a useable vocabulary\.
+ Your text file must be in `LF` format\. If you use any other format, such as `CRLF`, your custom vocabulary is not accepted by Amazon Transcribe\.

**Note**  
Enter acronyms, or other words whose letters should be pronounced individually, as single letters separated by periods \(**A\.B\.C\.**\)\. To enter the plural form of an acronym, such as 'ABCs', separate the 's' from the acronym with a hyphen \(**A\.B\.C\.\-s**\)\. You can use upper or lower case letters to define an acronym\. Acronyms are not supported in all languages; refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix)\.

Here is a sample custom vocabulary table \(where **\[TAB\]** represents a tab character\):

```
Phrase[TAB]SoundsLike[TAB]IPA[TAB]DisplayAs
Los-Angeles[TAB][TAB]l ɔ s æ n ʤ ə l ə s[TAB]Los Angeles
Eva-Maria [TAB]ay-va-ma-ree-ah[TAB][TAB]
A.B.C.-s[TAB]ay-bee-sees[TAB]ABCs
Amazon-dot-com[TAB][TAB][TAB]Amazon.com
C.L.I.[TAB][TAB]s ɪ ɛ l aɪ[TAB]CLI
Andorra-la-Vella[TAB]ann-do-rah-la-bey-ah[TAB][TAB]Andorra la Vella
Dynamo-D.B.[TAB][TAB][TAB]DynamoDB
```

Here is the same table with aligned columns for visual clarity\. **Do not** add spaces between columns in your vocabulary table; your table should look misaligned like the preceding example\.

```
Phrase          [TAB]SoundsLike          [TAB]IPA                [TAB]DisplayAs  
Los-Angeles     [TAB]                    [TAB]l ɔ s æ n ʤ ə l ə s[TAB]Los Angeles   
Eva-Maria       [TAB]ay-va-ma-ree-ah     [TAB]                   [TAB]
A.B.C.-s        [TAB]ay-bee-sees         [TAB]                   [TAB]ABCs  
amazon-dot-com  [TAB]                    [TAB]                   [TAB]amazon.com
C.L.I.          [TAB]                    [TAB]s ɪ ɛ l aɪ         [TAB]CLI   
Andorra-la-Vella[TAB]ann-do-rah-la-bey-ah[TAB]                   [TAB]Andorra la Vella
Dynamo-D.B.     [TAB]                    [TAB]                   [TAB]DynamoDB
```

To process a custom vocabulary table for use with Amazon Transcribe, see the following for examples:

## AWS Management Console<a name="clm-create-table-howto-console"></a>

Before continuing, save your vocabulary as a text \(\*\.txt\) file, then upload it into an S3 bucket\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Custom vocabulary**\. This opens the **Custom vocabulary** page where you can view existing vocabularies or create a new one\.

1. Select the **Create vocabulary** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console.png)

   This takes you to the **Create vocabulary** page\. Enter a name for your new vocabulary\.

   Select the **S3 location** option under **Vocabulary input source**\. Then, either manually enter the S3 path or select **Browse S3** to locate your vocabulary\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-s3.png)

1. Optionally, add tags to your vocabulary\. Once you have all fields completed, click the **Create vocabulary** button at the bottom of the page\. This takes you back to the **Custom vocabulary** page where you can view the status of your custom vocabulary\. When the status changes from 'Pending' to 'Ready' your vocabulary can be used with a transcription\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-pending.png)

1. If the status changes to 'Failed', click on the name of your vocabulary to go to its information page\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed.png)

   There is a **Failure reason** banner at the top of this page that provides information on why your vocabulary failed\. Correct the error in your text file and try again\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed2.png)

## AWS CLI<a name="vocab-create-table-howto-cli"></a>

This example uses the [create\-vocabulary](https://docs.aws.amazon.com/cli/latest/reference/transcribe/create-vocabulary.html) command with a table\-formatted vocabulary file\. For more information, see [CreateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

```
aws transcribe create-vocabulary \ 
--vocabulary-name my-first-vocabulary \ 
--vocabulary-file-uri s3://DOC-EXAMPLE-BUCKET/my-vocabulary-file.txt
--language-code en-US \
```

Here's another example using the [create\-vocabulary](https://docs.aws.amazon.com/cli/latest/reference/transcribe/create-vocabulary.html) command, and a request body that creates your vocabulary\.

```
aws transcribe create-vocabulary \
--cli-input-json file://filepath/my-first-vocab-table.json
```

The file *my\-first\-vocab\-table\.json* contains the following request body\.

```
{
  "VocabularyName": "my-first-vocabulary",
  "VocabularyFileUri": "s3://DOC-EXAMPLE-BUCKET/my-vocabulary-table.txt",
  "LanguageCode": "en-US"
}
```

Once `VocabularyState` changes from `PENDING` to `READY`, your vocabulary is ready to use with a transcription\. To view the current status of your vocabulary, run:

```
aws transcribe get-vocabulary \
--vocabulary-name my-first-vocabulary
```

## AWS SDK for Python \(Boto3\)<a name="vocab-create-table-howto-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to create a custom vocabulary from a table using the [create\_vocabulary](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_vocabulary) method\. For more information, see [CreateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe=boto3.client('transcribe', 'us-west-2')
job_name = "my-first-vocabulary"
response = transcribe.create_vocabulary(
    LanguageCode='en-US',
    VocabularyName=job_name,
    VocabularyFileUri='s3://DOC-EXAMPLE-BUCKET/my-vocabulary-table.txt'
)

while True:
    status = transcribe.get_vocabulary(VocabularyName=job_name)
    if status['VocabularyState'] in ['READY', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

To use an existing custom vocabulary in a transcription job, set the `VocabularyName` in the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html) field when you call the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) operation or, from the AWS Management Console, choose the vocabulary from the drop\-down list\.