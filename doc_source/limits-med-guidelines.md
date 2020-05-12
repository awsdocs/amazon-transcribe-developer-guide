# Guidelines and Quotas<a name="limits-med-guidelines"></a>

## Supported Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe Medical is available, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe-medical.html#transcribe_region) in the *Amazon Web Services General Reference*\.

## Throttling<a name="limits-med-throttling"></a>

You can request a quota increase for the following resources:


| Resource | Default | 
| --- | --- | 
| Number of concurrent batch transcription jobs | 100 | 
| Transactions per second, StartMedicalTranscriptionJob operation | 10 | 
| Number of StartMedicalStreamTranscription Websocket requests | 5 | 
| Transactions per second, StartMedicalStreamTranscription operation | 5 | 
| Transactions per second, GetMedicalTranscriptionJob operation | 20 | 
| Transactions per second, DeleteMedicalTranscriptionJob operation | 5 | 
| Transactions per second, ListMedicalTranscriptionJobs operation | 5 | 
| Transactions per second, CreateMedicalVocabulary operation | 10 | 
| Transactions per second, UpdateMedicalVocabulary operation | 10 | 
| Transactions per second, DeleteMedicalVocabulary operation | 5 | 
| Transactions per second, GetMedicalVocabulary operation | 20 | 
| Transactions per second, ListMedicalVocabularies operation | 5 | 

For information about requesting a quota increase, see [AWS Service Quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits-med.html) in the *Amazon Web Services General Reference*\.

## Guidelines<a name="guidelines-med"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 8000 Hz for low\-fidelity audio and 16000 Hz for high\-fidelity audio\.

Amazon Transcribe Medical may store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe Medical FAQ](https://aws.amazon.com/transcribe/faqs/) to learn more\. To request that we delete content that may have been stored by Amazon Transcribe Medical, open a case with AWS Support\.

## Quotas<a name="limits-med"></a>

Amazon Transcribe Medical has the following quotas that are not alterable:


| Description | Quotas | 
| --- | --- | 
| Maximum audio file length | 14,400 seconds | 
| Maximum audio file size | 2 GB | 
| Number of days that job records are retained | 90 | 
| Number of channels for channel identification | 2 | 
| Minimum audio file duration, in milliseconds \(ms\) | 500 | 