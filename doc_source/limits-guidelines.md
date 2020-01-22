# Guidelines and Quotas<a name="limits-guidelines"></a>

## Supported Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe is available, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region) in the *Amazon Web Services General Reference*\.

## Throttling<a name="limits-throttling"></a>

For information about throttling for Amazon Transcribe and to request a quota increase, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#limits-amazon-transcribe) in the *Amazon Web Services General Reference*\.

## Guidelines<a name="guidelines"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 8000 Hz for low\-fidelity audio and 16000 Hz for high\-fidelity audio\.

Amazon Transcribe may store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe FAQ](https://aws.amazon.com/transcribe/faqs/) to learn more\. To request that we delete content that may have been stored by Amazon Transcribe, open a case with AWS Support\.

## Quotas<a name="limits"></a>

Amazon Transcribe has the following quotas:


| Description | Quotas | 
| --- | --- | 
| Maximum audio file length | 7,200 seconds | 
| Maximum audio file size | 1 GB | 
| Maximum size of a custom vocabulary | 50 KB | 
| Maximum length of a custom vocabulary phrase | 256 characters | 
| Maximum size of a vocabulary filter | 5 MB | 
| Maximum number of vocabulary filters | 100 | 
| Number of days that job records are retained | 90 | 
| Number of channels for channel identification | 2 | 