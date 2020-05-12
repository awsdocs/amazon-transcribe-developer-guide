# Guidelines and Quotas<a name="limits-guidelines"></a>

## Supported Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe is available, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region) in the *Amazon Web Services General Reference*\.

## Throttling<a name="limits-throttling"></a>

You can request a quota increase for the following resources:


| Resource | Default | 
| --- | --- | 
| Number of concurrent batch transcription jobs | 100 | 
| Transactions per second, StartTranscriptionJob operation | 10 | 
| Number of concurrent HTTP/2 streams for streaming transcription | 5 | 
| Number of StartStreamTranscription Websocket requests | 5 | 
| Transactions per second, StartStreamTranscription operation | 5 | 
| Total number of vocabularies per account | 100 | 
| Number of pending vocabularies | 10 | 
| Transactions per second, GetTranscriptionJob operation | 20 | 
| Transactions per second, DeleteTranscriptionJob operation | 5 | 
| Transactions per second, ListTranscriptionJobs operation | 5 | 
| Transactions per second, CreateVocabulary and UpdateVocabulary operations | 10 | 
| Transactions per second, DeleteVocabulary operation | 5 | 
| Transactions per second, GetVocabulary operation | 20 | 
| Transactions per second, ListVocabularies operation | 5 | 

For information about requesting a quota increase, see [AWS Service Quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *Amazon Web Services General Reference*\.

## Guidelines<a name="guidelines"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 8000 Hz for low\-fidelity audio and 16000 Hz for high\-fidelity audio\.

Amazon Transcribe may store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe FAQ](https://aws.amazon.com/transcribe/faqs/) to learn more\. To request that we delete content that may have been stored by Amazon Transcribe, open a case with AWS Support\.

## Quotas<a name="limits"></a>

Amazon Transcribe has the following quotas that are not alterable:


| Description | Quotas | 
| --- | --- | 
| Maximum audio file length | 14,400 seconds | 
| Maximum audio file size | 2 GB | 
| Maximum size of a custom vocabulary | 50 KB | 
| Maximum length of a custom vocabulary phrase | 256 characters | 
| Maximum size of a vocabulary filter | 50 KB | 
| Maximum number of vocabulary filters | 100 | 
| Number of days that job records are retained | 90 | 
| Number of channels for channel identification | 2 | 
| Minimum audio file duration, in milliseconds \(ms\) | 500 | 