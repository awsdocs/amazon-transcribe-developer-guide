# Guidelines and quotas<a name="limits-med-guidelines"></a>

## Supported AWS Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe Medical is available, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe-medical.html#transcribe_region) in the *AWS General Reference*\.

## Guidelines<a name="guidelines-med"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 16,000 Hz or higher\.

Amazon Transcribe Medical may store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe Medical FAQ](http://aws.amazon.com/transcribe/faqs/) to learn more\. To request that we delete content that may have been stored by Amazon Transcribe Medical, open a case with AWS Support\.

## Quotas<a name="limits-med"></a>

You can request a quota increase for the following resources\.


| Resource | Default | 
| --- | --- | 
| Number of concurrent batch transcription jobs | 250 | 
| Number of concurrent HTTP/2 or WebSocket requests | 25 | 
| Total number of medical vocabularies per AWS account | 100 | 
| Number of pending medical vocabularies | 10 | 

The following API limits can also be increased upon request:


| API | Maximum transactions per second | 
| --- | --- | 
| [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) | 25 | 
| [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) | 25 | 
| [GetMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetMedicalTranscriptionJob.html) | 30 | 
| [DeleteMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteMedicalTranscriptionJob.html) | 5 | 
| [ListMedicalTranscriptionJobs](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListMedicalTranscriptionJobs.html) | 5 | 
| [CreateMedicalVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html) | 10 | 
| [UpdateMedicalVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateMedicalVocabulary.html) | 10 | 
| [DeleteMedicalVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteMedicalVocabulary.html) | 5 | 
| [GetMedicalVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetMedicalVocabulary.html) | 20 | 
| [ListMedicalVocabularies](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListMedicalVocabularies.html) | 5 | 

**Note**  
For information about requesting a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *AWS General Reference*\.

The following quotas **cannot** be increased:


| Description | Quotas | 
| --- | --- | 
| Maximum audio file length | 14,400 seconds | 
| Maximum audio file size | 2 GB | 
| Number of days that job records are retained | 90 | 
| Number of channels for channel identification | 2 | 
| Minimum audio file duration, in milliseconds \(ms\) | 500 | 