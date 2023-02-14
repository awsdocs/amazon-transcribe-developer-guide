# Creating a custom vocabulary using a table<a name="custom-vocabulary-create-table"></a>

Using a table format is the most robust way to create your custom vocabulary\. Vocabulary tables must consist of four columns, which can be included in any order:


| Phrase | SoundsLike | IPA | DisplayAs | 
| --- | --- | --- | --- | 
|  Required\. Every row in your table must contain an entry in this column\. Do not use spaces in this column\. If your entry contains multiple words, separate each word with a hyphen \(\-\)\. For example, **Andorra\-la\-Vella** or **Los\-Angeles**\. For acronyms, any pronounced letters must be separated by a period\. If your acronym is plural, you must use a hyphen between the acronym and the 's'\. For example, 'CLI' is **C\.L\.I\.** and 'ABCs' is **A\.B\.C\.\-s**\. If your phrase consists of both a word and an acronym, these two components must be separated by a hyphen\. For example, 'DynamoDB' is **Dynamo\-D\.B\.**\. Do not include digits in this column; numbers must be spelled out\. For example, 'VX02Q' is **V\.X\.\-zero\-two\-Q\.**\.  |  Optional\. Rows in this column can be left empty\. Do not use spaces in this column\. Include your entry as hyphen\-separated syllables that mimic how the word sounds\. It's better to use small, common words over phonetic representations\. For example, for 'Los Angeles', '**loss\-ann\-gel\-es**' is preferable to '**lahs\-ahn\-jul\-ees**'\. You cannot have an entry for both `SoundsLike` and `IPA` in the same row\.  |  Optional\. Rows in this column can be left empty\. You must add a single space between every IPA character \(single\-byte\) or valid IPA character pair \(double\-byte\)\. This column is intended for phonetic spellings using only characters in the [International Phonetic Alphabet \(IPA\)](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet)\. For example, 'Los Angeles' is **l ɔ s æ n ʤ ə l ə s** and 'CLI' is **s i ɛ l aɪ**\. You cannot have an entry for both `IPA` and `SoundsLike` in the same row\.  |  Optional\. Rows in this column can be left empty\. You can use spaces in this column\. Defines the how you want your entry to look in your transcription output\. For example, **Andorra\-la\-Vella** in the `Phrase` column is **Andorra la Vella** in the `DisplayAs` column\. If a row in this column is empty, Amazon Transcribe uses the contents of the `Phrase` column to determine output\. You can include digits \(`0-9`\) in this column\.  | 

Things to note when creating your table:
+ Your table must contain all four columns \(Phrase, SoundsLike, IPA, and DisplayAs\), but the `Phrase` column is the only one that must contain an entry on each row\. All other columns can be left empty\.
+ In a given row, you cannot have entries for both `IPA` and `SoundsLike` fields\. You must choose one or the other, or leave both blank\.
+ The `DisplayAs` column supports symbols and special characters \(for example, C\+\+\)\. All other columns support the characters that are listed on your language's [character set](charsets.md) page\.
+ If you want to include numbers in the `Phrase` column, you must spell them out\. Digits \(`0-9`\) are only supported in the `DisplayAs` column\.
+ Spaces are only allowed within the `IPA` and `DisplayAs` columns\. Do not use spaces to separate columns; columns must be TAB\-separated\.
+ You must save your table as a plain text \(\*\.txt\) file in `LF` format\. If you use any other format, such as `CRLF`, your custom vocabulary can't be processed\.
+ You must upload your custom vocabulary file into an Amazon S3 bucket and process it using [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html) before you can include it in a transcription request\. Refer to [Creating custom vocabulary tables](#custom-vocabulary-create-table-examples) for instructions\.

**Note**  
Enter acronyms, or other words whose letters should be pronounced individually, as single letters separated by periods \(**A\.B\.C\.**\)\. To enter the plural form of an acronym, such as 'ABCs', separate the 's' from the acronym with a hyphen \(**A\.B\.C\.\-s**\)\. You can use upper or lower case letters to define an acronym\. Acronyms are not supported in all languages; refer to [Supported languages and language\-specific features](supported-languages.md)\.

Here is a sample custom vocabulary table \(where **\[TAB\]** represents a tab character\):

```
Phrase[TAB]SoundsLike[TAB]IPA[TAB]DisplayAs
Los-Angeles[TAB][TAB]l ɔ s æ n ʤ ə l ə s[TAB]Los Angeles
Eva-Maria[TAB]ay-va-ma-ree-ah[TAB][TAB]
A.B.C.-s[TAB]ay-bee-sees[TAB][TAB]ABCs
Amazon-dot-com[TAB][TAB][TAB]Amazon.com
C.L.I.[TAB][TAB]s i ɛ l aɪ[TAB]CLI
Andorra-la-Vella[TAB]ann-do-rah-la-bay-ah[TAB][TAB]Andorra la Vella
Dynamo-D.B.[TAB][TAB][TAB]DynamoDB
V.X.-zero-two[TAB][TAB][TAB]VX02
V.X.-zero-two-Q.[TAB][TAB][TAB]VX02Q
```

For visual clarity, here is the same table with aligned columns\. **Do not** add spaces between columns in your custom vocabulary table; your table should look misaligned like the preceding example\.

```
Phrase          [TAB]SoundsLike          [TAB]IPA                [TAB]DisplayAs  
Los-Angeles     [TAB]                    [TAB]l ɔ s æ n ʤ ə l ə s[TAB]Los Angeles   
Eva-Maria       [TAB]ay-va-ma-ree-ah     [TAB]                   [TAB]
A.B.C.-s        [TAB]ay-bee-sees         [TAB]                   [TAB]ABCs  
amazon-dot-com  [TAB]                    [TAB]                   [TAB]amazon.com
C.L.I.          [TAB]                    [TAB]s i ɛ l aɪ         [TAB]CLI   
Andorra-la-Vella[TAB]ann-do-rah-la-bay-ah[TAB]                   [TAB]Andorra la Vella
Dynamo-D.B.     [TAB]                    [TAB]                   [TAB]DynamoDB
V.X.-zero-two   [TAB]                    [TAB]                   [TAB]VX02
V.X.-zero-two-Q.[TAB]                    [TAB]                   [TAB]VX02Q
```

## Creating custom vocabulary tables<a name="custom-vocabulary-create-table-examples"></a>

To process a custom vocabulary table for use with Amazon Transcribe, see the following examples:

### AWS Management Console<a name="vocab-create-table-console"></a>

Before continuing, save your custom vocabulary as a text \(\*\.txt\) file, then upload it into an Amazon S3 bucket\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Custom vocabulary**\. This opens the **Custom vocabulary** page where you can view existing vocabularies or create a new one\.

1. Select **Create vocabulary**\.  
![\[Amazon Transcribe console screenshot: the 'custom vocabulary' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console.png)

   This takes you to the **Create vocabulary** page\. Enter a name for your new custom vocabulary\.

   Select the **S3 location** option under **Vocabulary input source**\. Then, either manually enter the Amazon S3 path or select **Browse S3** to locate your custom vocabulary\.  
![\[Amazon Transcribe console screenshot: the 'create vocabulary' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-s3.png)

1. Optionally, add tags to your custom vocabulary\. Once you have all fields completed, select **Create vocabulary** at the bottom of the page\. This takes you back to the **Custom vocabulary** page where you can view the status of your custom vocabulary\. When the status changes from 'Pending' to 'Ready' your custom vocabulary can be used with a transcription\.  
![\[Amazon Transcribe console screenshot: custom vocabulary in pending status while processing.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-pending.png)

1. If the status changes to 'Failed', click on the name of your custom vocabulary to go to its information page\.  
![\[Amazon Transcribe console screenshot: 'custom vocabulary' page showing one vocabulary as complete and one as failed.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed.png)

   There is a **Failure reason** banner at the top of this page that provides information on why your custom vocabulary failed\. Correct the error in your text file and try again\.  
![\[Amazon Transcribe console screenshot: vocabulary's information page shows failure reason.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed2.png)

### AWS CLI<a name="vocab-create-table-cli"></a>

This example uses the [create\-vocabulary](https://docs.aws.amazon.com/cli/latest/reference/transcribe/create-vocabulary.html) command with a table\-formatted vocabulary file\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

To use an existing custom vocabulary in a transcription job, set the `VocabularyName` in the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html) field when you call the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) operation or, from the AWS Management Console, choose the custom vocabulary from the drop\-down list\.

```
aws transcribe create-vocabulary \ 
--vocabulary-name my-first-vocabulary \ 
--vocabulary-file-uri s3://DOC-EXAMPLE-BUCKET/my-vocabularies/my-vocabulary-file.txt \
--language-code en-US
```

Here's another example using the [create\-vocabulary](https://docs.aws.amazon.com/cli/latest/reference/transcribe/create-vocabulary.html) command, and a request body that creates your custom vocabulary\.

```
aws transcribe create-vocabulary \
--cli-input-json file://filepath/my-first-vocab-table.json
```

The file *my\-first\-vocab\-table\.json* contains the following request body\.

```
{
  "VocabularyName": "my-first-vocabulary",
  "VocabularyFileUri": "s3://DOC-EXAMPLE-BUCKET/my-vocabularies/my-vocabulary-table.txt",
  "LanguageCode": "en-US"
}
```

Once `VocabularyState` changes from `PENDING` to `READY`, your custom vocabulary is ready to use with a transcription\. To view the current status of your custom vocabulary, run:

```
aws transcribe get-vocabulary \
--vocabulary-name my-first-vocabulary
```

### AWS SDK for Python \(Boto3\)<a name="vocab-create-table-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to create a custom vocabulary from a table using the [create\_vocabulary](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_vocabulary) method\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

To use an existing custom vocabulary in a transcription job, set the `VocabularyName` in the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html) field when you call the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) operation or, from the AWS Management Console, choose the custom vocabulary from the drop\-down list\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe using AWS SDKs](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
vocab_name = "my-first-vocabulary"
response = transcribe.create_vocabulary(
    LanguageCode = 'en-US',
    VocabularyName = vocab_name,
    VocabularyFileUri = 's3://DOC-EXAMPLE-BUCKET/my-vocabularies/my-vocabulary-table.txt'
)

while True:
    status = transcribe.get_vocabulary(VocabularyName = vocab_name)
    if status['VocabularyState'] in ['READY', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

**Note**  
If you create a new Amazon S3 bucket for your custom vocabulary files, make sure the IAM role making the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html) request has permissions to access this bucket\. If the role doesn't have the correct permissions, your request fails\. You can optionally specify an IAM role within your request by including the `DataAccessRoleArn` parameter\. For more information on IAM roles and policies in Amazon Transcribe, see [Amazon Transcribe identity\-based policy examples](security_iam_id-based-policy-examples.md)\.