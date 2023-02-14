# Guidelines and quotas<a name="limits-guidelines"></a>

Amazon Transcribe has several guidelines to follow in order to achieve optimal results\. There are also quotas that may impact your transcriptions; some of these can be increased\. Refer to the following sections for details\.

## Supported AWS Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe is available, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region) in the *AWS General Reference*\.

## Guidelines<a name="guidelines"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV with PCM 16\-bit encoding\.
+ Use a sample rate of 8,000 Hz for low\-fidelity audio and 16,000\-48,000 Hz for high\-fidelity audio\.

If you don't need to process all of your transcription jobs concurrently, use [Job queueing](job-queueing.md)\. This enables Amazon Transcribe to keep track of your transcription jobs and process them when slots are available\.

**Note**  
Amazon Transcribe may temporarily store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe FAQ](http://aws.amazon.com/transcribe/faqs/) to learn more\. To request the deletion of content that may have been stored by Amazon Transcribe, open a case with [AWS Support](http://aws.amazon.com/contact-us/)\.

## Quotas<a name="limits"></a>

The following quotas **cannot** be changed:


| Description | Quota | 
| --- | --- | 
| Audio file length | 4:00:00 \(four\) hours \(14,400 seconds\) | 
| Audio stream duration | 4:00:00 \(four\) hours \(14,400 seconds\) | 
| Audio file size | 2 GB | 
| Audio file size \(Call Analytics\) | 500 MB | 
| Size of a custom vocabulary | 50 KB | 
| Length of a custom vocabulary phrase | 256 characters | 
| Size of a custom vocabulary filter | 50 KB | 
| Number of custom vocabulary filters | 100 | 
| Number of channels for channel identification | 2 | 
| Number of days job records are retained | 90 | 
| Minimum audio file duration | 500 milliseconds \(ms\) | 

The following quotas **can** be increased upon request:


| Resource | Default | 
| --- | --- | 
| Number of concurrent batch transcription jobs | 250 | 
| Number of concurrent batch transcription jobs \(Call Analytics\) | 100 | 
| Job queue bandwidth ratio | 0\.9 | 
| Number of concurrent HTTP/2 requests | 25 | 
| Number of concurrent WebSocket requests | 25 | 
| Total number of vocabularies per AWS account | 100 | 
| Number of pending vocabularies | 10 | 
| Number of concurrently training custom language models | 3 | 
| Total number of custom language models per AWS account | 10 | 
| Number of categories per AWS account \(Call Analytics\) | 200 | 
| Number of rules per category \(Call Analytics\) | 20 | 

The following operations limits can also be increased upon request:


| Operation | Transactions per second | 
| --- | --- | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) | 25 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) | 25 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetTranscriptionJob.html) | 30 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteTranscriptionJob.html) | 5 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListTranscriptionJobs.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListTranscriptionJobs.html) | 5 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html) | 10 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateVocabulary.html) | 10 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteVocabulary.html) | 5 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabulary.html) | 20 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularies.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularies.html) | 5 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html) | 10 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsJob.html) | 20 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsJobs.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsJobs.html) | 5 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsJob.html) | 5 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html) | 10 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateCallAnalyticsCategory.html) | 10 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsCategory.html) | 5 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsCategory.html) | 20 | 
| [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsCategories.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsCategories.html) | 5 | 

**Note**  
For information about requesting a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *AWS General Reference*\.