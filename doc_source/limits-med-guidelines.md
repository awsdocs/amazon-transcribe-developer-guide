# Guidelines and quotas<a name="limits-med-guidelines"></a>

## Supported Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe Medical is available, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe-medical.html#transcribe_region) in the *Amazon Web Services General Reference*\.

## Guidelines<a name="guidelines-med"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 16,000 Hz or greater\.

Amazon Transcribe Medical may store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe Medical FAQ](http://aws.amazon.com/transcribe/faqs/) to learn more\. To request that we delete content that may have been stored by Amazon Transcribe Medical, open a case with AWS Support\.

## Quotas<a name="limits-med"></a>

You can request a quota increase for the following resources\.


| Resource | Default | 
| --- | --- | 
| Number of concurrent batch transcription jobs | 250 | 
| Number of [StartMedicalStreamTranscription](API_streaming_StartMedicalStreamTranscription.md) or Websocket requests | 25 | 
| Total number of medical vocabularies per account | 100 | 
| Number of pending medical vocabularies | 10 | 

The below API limits can also be increased upon request:


| API | Maximum transactions per second | 
| --- | --- | 
| [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) | 25 | 
| [StartMedicalStreamTranscription](API_streaming_StartMedicalStreamTranscription.md) | 25 | 
| [GetMedicalTranscriptionJob](API_GetMedicalTranscriptionJob.md) | 30 | 
| [DeleteMedicalTranscriptionJob](API_DeleteMedicalTranscriptionJob.md) | 5 | 
| [ListMedicalTranscriptionJobs](API_ListMedicalTranscriptionJobs.md) | 5 | 
| [CreateMedicalVocabulary](API_CreateMedicalVocabulary.md) | 10 | 
| [UpdateMedicalVocabulary](API_UpdateMedicalVocabulary.md) | 10 | 
| [DeleteMedicalVocabulary](API_DeleteMedicalVocabulary.md) | 5 | 
| [GetMedicalVocabulary](API_GetMedicalVocabulary.md) | 20 | 
| [ListMedicalVocabularies](API_ListMedicalVocabularies.md) | 5 | 

**Note**  
For information about requesting a quota increase, see [AWS Service Quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *Amazon Web Services General Reference*\.

The following quotas **cannot** be increased:


| Description | Quotas | 
| --- | --- | 
| Maximum audio file length | 14,400 seconds | 
| Maximum audio file size | 2 GB | 
| Number of days that job records are retained | 90 | 
| Number of channels for channel identification | 2 | 
| Minimum audio file duration, in milliseconds \(ms\) | 500 | 