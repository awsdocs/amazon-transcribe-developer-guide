# Language identification with batch transcription jobs<a name="lang-id-batch"></a>

Use language identification with batch jobs to identify the dominant language in your media file\. If your media file contains multiple languages, your transcription is created based on only the dominant language\.

To improve language identification accuracy, you can provide a list of languages you think may be present\. From this list, Amazon Transcribe chooses the closest matching language to transcribe your audio\. If none of the language codes you provide match languages spoken in your media, your transcription accuracy is diminished—this is because Amazon Transcribe prioritizes the languages you select\. Although there is no limit on the number of language codes you can include, we recommend using five or less for optimal efficiency and accuracy\.

**Tip**  
Providing a subset of language options is particularly helpful in transcribing regional dialects\. For example, if you know your media file contains an English dialect from the United Kingdom, but you're not sure which accent is present, provide Amazon Transcribe with `en-GB`, `en-AB`, and `en-WL` and omit the other English language codes\.

Here's an example of what confidence scores look like using a media file with one New Zealand English speaker and one US English speaker:


| Without any language codes provided | With language codes \(en\-US, en\-NZ, en\-AU\) provided | 
| --- | --- | 
|  <pre> "language_identification": [<br />            {<br />                "score": "0.4633",<br />                "code": "en-NZ"<br />            },<br />            {<br />                "score": "0.2386",<br />                "code": "en-US"<br />            },<br />            {<br />                "score": "0.1711",<br />                "code": "en-AU"<br />            },<br />            {<br />                "score": "0.0662",<br />                "code": "en-IE"<br />            },<br />            {<br />                "score": "0.0607",<br />                "code": "en-ZA"<br />            }<br />        ],</pre>  |  <pre>"language_identification": [<br />            {<br />                "score": "0.5336",<br />                "code": "en-NZ"<br />            },<br />            {<br />                "score": "0.2681",<br />                "code": "en-US"<br />            },<br />            {<br />                "score": "0.1983",<br />                "code": "en-AU"<br />            }<br />        ],</pre>  | 

As you can see in the preceding table, specifying at least one language code improves language identification confidence levels\.

You can use batch language identification in combination with any other Amazon Transcribe feature\. If combining language identification with another feature, you are limited to the languages supported with those features\.

**Important**  
If you're using automatic language identification with content redaction enabled, make sure that the language of your media file is [supported with redaction](supported-languages.md#table-language-matrix)\. If the language in your file is not supported, your transcript is **not** redacted and there are no warnings or job failures\.

If using language identification with a language model, vocabulary filter, or custom vocabulary, you must use the [LanguageIdSettings](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_LanguageIdSettings.html) parameter in your request\. Using this parameter, you can specify one language model, one vocabulary filter, and one custom vocabulary for every language code you provide\. Note that the language codes for each must match the language codes you specify in your request\. For an example of what this parameter looks like in a request, refer to Option 2 in the **AWS CLI** and **AWS SDK** drop\-down panels\.

For best results, ensure your media file contains at least 30 seconds of speech\.

You can use automatic language identification in a batch transcription job using the **AWS Management Console**, **AWS CLI**, or **AWS SDK**; see the following for examples:

## AWS Management Console<a name="lang-howto-console-batch"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This opens the **Specify job details** page\.

1. In the **Job settings** panel, find the **Language settings** section and select **Automatic language identification**\. You also have the option to select multiple languages \(from the *Select languages* drop\-down box\) if you have an idea of which language your file contains\. This option can improve accuracy, but is not required\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-batch1.png)

1. Fill in any other fields you wish to include on the **Specify job details** page, then click the **Next** button\. This takes you to the **Configure job \- *optional*** page\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-configure-batch.png)

1. Click the **Create job** button to run your transcription job\. 

## AWS CLI<a name="lang-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `IdentifyLanguage` parameter\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [LanguageIdSettings](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_LanguageIdSettings.html)\.

**Option 1**: Without the `language-id-settings` parameter\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--identify-language
```

**Option 2**: With the `language-id-settings` parameter\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--identify-language --language-id-settings "{\"en-US\":{\"VocabularyName\":\"my-en-US-vocabulary\",
\"VocabularyFilterName\":\"my-en-US-vocabulary-filter\",\"LanguageModelName\":\"my-en-US-language-model\"},
\"en-AU\":{\"VocabularyName\":\"my-en-AU-vocabulary\"}}
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that identifies the language\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--cli-input-json file://filepath/my-first-language-id-job.json
```

The file *my\-first\-language\-id\-job\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "my-first-transcription-job",  
  "Media": {
        "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
   },
  "OutputBucketName": "DOC-EXAMPLE-BUCKET",
  "IdentifyLanguage": "true"
}
```

## AWS SDK for Python \(Boto3\)<a name="lang-howto-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to identify your file's language using the `IdentifyLanguage` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [LanguageIdSettings](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_LanguageIdSettings.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe](service_code_examples.md) chapter\.

**Option 1**: Without the `LanguageIdSettings` parameter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-transcription-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
transcribe.start_transcription_job(
    TranscriptionJobName=job_name,
    Media={
        'MediaFileUri': job_uri
        },
    MediaFormat='flac',
    IdentifyLanguage=True
)

while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

**Option 2**: With the `LanguageIdSettings` parameter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "my-first-transcription-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
transcribe.start_transcription_job(
    TranscriptionJobName=job_name,
    Media={'MediaFileUri': job_uri},
    MediaFormat='flac',
    IdentifyLanguage=True,
    LanguageIdSettings={
        'en-US': {
            'VocabularyName': 'my-en-US-vocabulary',
            'VocabularyFilterName': 'my-en-US-vocabulary-filter',
            'LanguageModelName': 'my-en-US-language-model'
        }
    }
)
while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```