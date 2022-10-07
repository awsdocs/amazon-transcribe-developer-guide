# Creating a custom vocabulary using a list<a name="custom-vocabulary-create-list"></a>

You can create custom vocabularies from lists using the AWS Management Console, AWS CLI, or AWS SDKs\.
+ **AWS Management Console**: You must create and upload a text file containing your custom vocabulary\. You can use either line\-separated or comma\-separated entries\. Note that your list must be saved as a text \(\*\.txt\) file in `LF` format\. If you use any other format, such as `CRLF`, your custom vocabulary is not accepted by Amazon Transcribe\.
+ **AWS CLI** and **AWS SDKs**: You must include your custom vocabulary as comma\-separated entries within your API call using the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html#transcribe-CreateVocabulary-request-Phrases](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html#transcribe-CreateVocabulary-request-Phrases) flag\.

If an entry contains multiple words, you must hyphenate each word\. For example, you include 'Los Angeles' as **Los\-Angeles** and 'Andorra la Vella' as **Andorra\-la\-Vella**\.

Here are examples of the two valid list formats\. Refer to [Creating custom vocabulary lists](#custom-vocabulary-create-list-examples) for method\-specific examples\.
+ Comma\-separated entries:

  ```
  Los-Angeles,CLI,Eva-Maria,ABCs,Andorra-la-Vella
  ```
+ Line\-separated entries:

  ```
  Los-Angeles
  CLI
  Eva-Maria
  ABCs
  Andorra-la-Vella
  ```

**Important**  
You can only use characters that are supported for your language\. Refer to your language's [character set](charsets.md) for details\.

Custom vocabulary lists are not supported with the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html) operation\. If creating a custom medical vocabulary, you must use a table format; refer to [Creating a custom vocabulary using a table](custom-vocabulary-create-table.md) for instructions\.

## Creating custom vocabulary lists<a name="custom-vocabulary-create-list-examples"></a>

To process a custom vocabulary list for use with Amazon Transcribe, see the following examples:

### AWS Management Console<a name="vocab-create-list-console-batch"></a>

Before continuing, save your custom vocabulary as a text \(\*\.txt\) file\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Custom vocabulary**\. This opens the **Custom vocabulary** page where you can view existing vocabularies or create a new one\.

1. Select **Create vocabulary**\.  
![\[Amazon Transcribe console screenshot: the custom vocabulary main page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console.png)

   This takes you to the **Create vocabulary** page\. Enter a name for your new custom vocabulary\.

   Select the **File upload** option under **Vocabulary input source**\. Then, select **Choose file** to upload your custom vocabulary\.  
![\[Amazon Transcribe console screenshot: the 'create vocabulary' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-upload.png)

1. Optionally, add tags to your custom vocabulary\. Once you have all fields completed, select **Create vocabulary** at the bottom of the page\. This takes you back to the **Custom vocabulary** page where you can view the status of your custom vocabulary\. When the status changes from 'Pending' to 'Ready' your custom vocabulary can be used with a transcription\.  
![\[Amazon Transcribe console screenshot: custom vocabulary in pending status while processing.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-pending.png)

1. If the status changes to 'Failed', click on the name of your custom vocabulary to go to its information page\.  
![\[Amazon Transcribe console screenshot: 'custom vocabulary' page showing one vocabulary as complete and one as failed.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed.png)

   There is a **Failure reason** banner at the top of this page that provides information on why your custom vocabulary failed\. Correct the error in your text file and try again\.  
![\[Amazon Transcribe console screenshot: vocabulary's information page shows failure reason.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed2.png)

### AWS CLI<a name="vocab-create-list-cli"></a>

This example uses the [create\-vocabulary](https://docs.aws.amazon.com/cli/latest/reference/transcribe/create-vocabulary.html) command with a list\-formatted custom vocabulary file\. For more information, see [CreateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

```
aws transcribe create-vocabulary \ 
--vocabulary-name my-first-vocabulary \ 
--language-code en-US \ 
--phrases {CLI,Eva-Maria,ABCs}
```

Here's another example using the [create\-vocabulary](https://docs.aws.amazon.com/cli/latest/reference/transcribe/create-vocabulary.html) command, and a request body that creates your vocabulary\.

```
aws transcribe create-vocabulary \
--cli-input-json file://filepath/my-first-vocab-list.json
```

The file *my\-first\-vocab\-list\.json* contains the following request body\.

```
{
  "VocabularyName": "my-first-vocabulary",
  "LanguageCode": "en-US",
  "Phrases": [
        "CLI","Eva-Maria","ABCs"
  ]
}
```

Once `VocabularyState` changes from `PENDING` to `READY`, your custom vocabulary is ready to use with a transcription\. To view the current status of your custom vocabulary, run:

```
aws transcribe get-vocabulary \
--vocabulary-name my-first-vocabulary
```

### AWS SDK for Python \(Boto3\)<a name="vocab-create-list-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to create a custom vocabulary from a list using the [create\_vocabulary](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_vocabulary) method\. For more information, see [CreateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

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
    Phrases = [
        'CLI','Eva-Maria','ABCs'
    ]
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