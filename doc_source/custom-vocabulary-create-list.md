# Creating a custom vocabulary using a list<a name="custom-vocabulary-create-list"></a>

You can create custom vocabularies from lists using the AWS Management Console, AWS CLI, or AWS SDKs\.

If using the [AWS Management Console](https://console.aws.amazon.com/transcribe/), you must create a text file for your vocabulary list\. You can either place each entry on its own line, or put multiple entries on a single line, separating each entry with a comma\. Note that if your entry is a phrase, you must hyphenate each word; for example, 'Los Angeles' looks like **Los\-Angeles** and 'Andorra la Vella' looks like **Andorra\-la\-Vella**\.

Here are examples of valid lists:

```
Los-Angeles,CLI,Eva-Maria,ABCs,Andorra-la-Vella
```

```
Los-Angeles
CLI
Eva-Maria
ABCs
Andorra-la-Vella
```

If using the CLI or an SDK to create your vocabulary, you must include your entries within the API call using the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html#transcribe-CreateVocabulary-request-Phrases](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html#transcribe-CreateVocabulary-request-Phrases) flag\.

Things to note when creating your list:
+ You can only use characters that are supported for your language\. Refer to your language's [character set](charsets.md) for details\.
+ If using the AWS Management Console, you must save your list as a text \(\*\.txt\) file in `LF` format\. If you use any other format, such as `CRLF`, your custom vocabulary is not accepted by Amazon Transcribe\.

**Note**  
Vocabulary lists are not supported with the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html) operation\.

To process a custom vocabulary list for use with Amazon Transcribe, see the following for examples:

## AWS Management Console<a name="clm-create-list-howto-console"></a>

Before continuing, save your vocabulary as a text \(\*\.txt\) file\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Custom vocabulary**\. This opens the **Custom vocabulary** page where you can view existing vocabularies or create a new one\.

1. Select the **Create vocabulary** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console.png)

   This takes you to the **Create vocabulary** page\. Enter a name for your new vocabulary\.

   Select the **File upload** option under **Vocabulary input source**\. Then, select **Choose file** to upload your vocabulary\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-upload.png)

1. Optionally, add tags to your vocabulary\. Once you have all fields completed, click the **Create vocabulary** button at the bottom of the page\. This takes you back to the **Custom vocabulary** page where you can view the status of your custom vocabulary\. When the status changes from 'Pending' to 'Ready' your vocabulary can be used with a transcription\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-pending.png)

1. If the status changes to 'Failed', click on the name of your vocabulary to go to its information page\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed.png)

   There is a **Failure reason** banner at the top of this page that provides information on why your vocabulary failed\. Correct the error in your text file and try again\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/vocab-create-console-failed2.png)

## AWS CLI<a name="vocab-create-list-howto-cli"></a>

This example uses the [create\-vocabulary](https://docs.aws.amazon.com/cli/latest/reference/transcribe/create-vocabulary.html) command with a list\-formatted vocabulary file\. For more information, see [CreateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

```
aws transcribe create-vocabulary \ 
--vocabulary-name my-first-vocabulary \ 
--language-code en-US \ 
--phrases {
    CLI,Eva-Maria,ABCs
  }
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

Once `VocabularyState` changes from `PENDING` to `READY`, your vocabulary is ready to use with a transcription\. To view the current status of your vocabulary, run:

```
aws transcribe get-vocabulary \
--vocabulary-name my-first-vocabulary
```

## AWS SDK for Python \(Boto3\)<a name="vocab-create-list-howto-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to create a custom vocabulary from a list using the [create\_vocabulary](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_vocabulary) method\. For more information, see [CreateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html)\.

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
    Phrases=[
        'CLI','Eva-Maria','ABCs'
    ]
)

while True:
    status = transcribe.get_vocabulary(VocabularyName=job_name)
    if status['VocabularyState'] in ['READY', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```