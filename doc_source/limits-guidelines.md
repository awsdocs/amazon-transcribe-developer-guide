# Guidelines and Limits<a name="limits-guidelines"></a>

## Supported Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe is available, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region) in the *Amazon Web Services General Reference*\.

## Throttling<a name="limits-throttling"></a>

For information about throttling for Amazon Transcribe and to request a limit increase, see [Amazon Transcribe Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html#limits-amazon-transcribe) in the *Amazon Web Services General Reference*\.

## Guidelines<a name="guidelines"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 8000 Hz for low\-fidelity audio and 16000 Hz for high\-fidelity audio\.

Amazon Transcribe may store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe FAQ](https://aws.amazon.com/transcribe/faqs/) to learn more\. To request that we delete content that may have been stored by Amazon Transcribe, open a case with AWS Support\.

## Limits<a name="limits"></a>

Amazon Transcribe has the following limitations:


| Description | Limit | 
| --- | --- | 
| Maximum audio file length | 4 hours | 
| Maximum audio file size | 2 GB | 
| Maximum size of a custom vocabulary | 50 KB | 
| Maximum length of a custom vocabulary phrase | 256 characters | 