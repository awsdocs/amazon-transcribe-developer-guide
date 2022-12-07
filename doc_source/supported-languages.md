# Supported languages and language\-specific features<a name="supported-languages"></a>

The languages supported by Amazon Transcribe are listed in the following table; also listed are the features that are language\-specific\. Please verify that the feature you want to use is supported for the language in your media before proceeding with your transcription\.

To view the complete list of Amazon Transcribe features, refer to the [Feature summary](feature-matrix.md)\.

In the following table, 'batch' refers to transcribing a media file located in an Amazon S3 bucket and 'streaming' refers to transcribing streamed media in real time\. For Call Analytics transcriptions, 'post\-call' refers to transcribing a media file located in an Amazon S3 bucket and 'real\-time' refers to transcribing streamed media in real time\. 


|  **Language**  |  **Language Code**  |  **[Data input](how-input.md)**  |  **[Transcribing numbers](how-numbers.md)**  |  **[Acronyms](custom-vocabulary-create-table.md)**  |  **[Custom language models](custom-language-models.md)**  |  **[Redaction](pii-redaction.md)**  |  **[Call Analytics](call-analytics.md)**  | 
| --- | --- | --- | --- | --- | --- | --- | --- | 
| [Afrikaans](charsets.md#char-afrikaans) | af\-ZA | batch | no | batch | no | no | no | 
| [Arabic](charsets.md#char-arabic), Gulf | ar\-AE | batch | no | no | no | no | post\-call | 
| [Arabic](charsets.md#char-arabic), Modern Standard | ar\-SA | batch | no | no | no | no | no | 
| [Chinese, Simplified](charsets.md#char-chinese-man-cn) | zh\-CN | batch, streaming | no | no | no | no | post\-call | 
| [Chinese, Traditional](charsets.md#char-chinese-man-tw) | zh\-TW | batch | no | no | no | no | no | 
| [Danish](charsets.md#char-danish) | da\-DK | batch | no | batch | no | no | no | 
| [Dutch](charsets.md#char-dutch) | nl\-NL | batch | no | batch | no | no | no | 
| [English](charsets.md#char-english), Australian | en\-AU | batch, streaming | batch, streaming | batch, streaming | batch, streaming | streaming | post\-call, real\-time | 
| [English](charsets.md#char-english), British | en\-GB | batch, streaming | batch, streaming | batch, streaming | batch, streaming | streaming | post\-call, real\-time | 
| [English](charsets.md#char-english), Indian | en\-IN | batch | batch | batch | no | no | post\-call | 
| [English](charsets.md#char-english), Irish | en\-IE | batch | batch | batch | no | no | post\-call | 
| [English](charsets.md#char-english), New Zealand | en\-NZ | batch | batch | batch | no | no | no | 
| [English](charsets.md#char-english), Scottish | en\-AB | batch | batch | batch | no | no | post\-call | 
| [English](charsets.md#char-english), South African | en\-ZA | batch | batch | batch | no | no | no | 
| [English](charsets.md#char-english), US | en\-US | batch, streaming | batch, streaming | batch, streaming | batch, streaming | batch, streaming | post\-call, real\-time | 
| [English](charsets.md#char-english), Welsh | en\-WL | batch | batch | batch | no | no | post\-call | 
| [French](charsets.md#char-french) | fr\-FR | batch, streaming | no | batch, streaming | no | no | post\-call, real\-time | 
| [French](charsets.md#char-french), Canadian | fr\-CA | batch, streaming | no | batch, streaming | no | no | post\-call, real\-time | 
| [Farsi](charsets.md#char-farsi) | fa\-IR | batch | no | no | no | no | no | 
| [German](charsets.md#char-german) | de\-DE | batch, streaming | batch, streaming | batch, streaming | batch, streaming | no | post\-call, real\-time | 
| [German](charsets.md#char-german), Swiss | de\-CH | batch | batch | batch | no | no | post\-call | 
| [Hebrew](charsets.md#char-hebrew) | he\-IL | batch | no | no | no | no | no | 
| [Hindi](charsets.md#char-hindi), Indian | hi\-IN | batch, streaming | no | batch, streaming | batch | no | post\-call | 
| [Indonesian](charsets.md#char-indonesian) | id\-ID | batch | no | batch | no | no | no | 
| [Italian](charsets.md#char-italian) | it\-IT | batch, streaming | no | batch, streaming | no | no | post\-call, real\-time | 
| [Japanese](charsets.md#char-japanese) | ja\-JP | batch, streaming | no | no | batch, streaming | no | post\-call | 
| [Korean](charsets.md#char-korean) | ko\-KR | batch, streaming | no | no | no | no | post\-call | 
| [Malay](charsets.md#char-malay) | ms\-MY | batch | no | batch | no | no | no | 
| [Portuguese](charsets.md#char-portuguese) | pt\-PT | batch | no | batch | no | no | post\-call | 
| [Portuguese](charsets.md#char-portuguese), Brazilian | pt\-BR | batch, streaming | no | batch, streaming | no | no | post\-call, real\-time | 
| [Russian](charsets.md#char-russian) | ru\-RU | batch | no | no | no | no | no | 
| [Spanish](charsets.md#char-spanish) | es\-ES | batch | no | batch | no | no | post\-call | 
| [Spanish](charsets.md#char-spanish), US | es\-US | batch, streaming | no | batch, streaming | batch, streaming | no | post\-call, real\-time | 
| [Tamil](charsets.md#char-tamil) | ta\-IN | batch | no | no | no | no | no | 
| [Telugu](charsets.md#char-telugu) | te\-IN | batch | no | no | no | no | no | 
| [Thai](charsets.md#char-thai) | th\-TH | batch, streaming | no | batch, streaming | no | no | no | 
| [Turkish](charsets.md#char-turkish) | tr\-TR | batch | no | batch | no | no | no | 

## Supported programming languages<a name="supported-sdks"></a>

Amazon Transcribe supports the following AWS SDKs:


| Batch transcriptions | Streaming transcriptions | 
| --- | --- | 
| [AWS Command Line Interface \(CLI\)](https://docs.aws.amazon.com/cli/latest/reference/transcribe/index.html#cli-aws-transcribe) | The CLI is not supported for streaming\. | 
| [C\+\+](https://sdk.amazonaws.com/cpp/api/LATEST/namespace_aws_1_1_transcribe_service.html) | [C\+\+](https://github.com/aws/aws-sdk-cpp/tree/master/aws-cpp-sdk-transcribestreaming) | 
| [Go](https://docs.aws.amazon.com/sdk-for-go/api/service/transcribeservice/) | [Go](https://docs.aws.amazon.com/sdk-for-go/api/service/transcribestreamingservice/) | 
| [Java V2](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/transcribe/TranscribeClient.html) | [Java V2](https://github.com/aws/aws-sdk-java-v2/tree/master/services/transcribestreaming) | 
| [JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/TranscribeService.html) | [JavaScript V3](https://github.com/aws/aws-sdk-js-v3/tree/master/clients/client-transcribe-streaming) | 
| [PHP V3](https://docs.aws.amazon.com/aws-sdk-php/v3/api/namespace-Aws.TranscribeService.html) | [PHP V3](https://github.com/aws/aws-sdk-php/releases/tag/3.172.4) | 
| [Python Boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html) | [Python Streaming SDK for Amazon Transcribe](https://github.com/awslabs/amazon-transcribe-streaming-sdk) | 
| [Ruby V3](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/TranscribeService.html) | [Ruby V3](https://github.com/aws/aws-sdk-ruby/tree/version-3/gems/aws-sdk-transcribestreamingservice) | 
| [\.NET](https://docs.aws.amazon.com/sdkfornet/v3/apidocs/items/TranscribeService/NTranscribeService.html) | \.NET is not supported for streaming\. | 

For more information on using SDKs with Amazon Transcribe, refer to [Transcribing with the AWS SDKs](getting-started-sdk.md)\.