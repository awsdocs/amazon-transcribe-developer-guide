# Guidelines and quotas<a name="limits-guidelines"></a>

Amazon Transcribe has several guidelines to follow in order to achieve optimal results\. There are also quotas that may impact your transcriptions; some of these can be increased\. Refer to the following sections for details\.

## Supported Regions<a name="transcribe-regions"></a>

For a list of AWS Regions where Amazon Transcribe is available, see [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region) in the *Amazon Web Services General Reference*\.

## Guidelines<a name="guidelines"></a>

For best results:
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 8,000 Hz for low\-fidelity audio and 16,000 Hz \(or higher\) for high\-fidelity audio\.

**Note**  
Amazon Transcribe may temporarily store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe FAQ](http://aws.amazon.com/transcribe/faqs/) to learn more\. To request that we delete content that may have been stored by Amazon Transcribe, open a case with [AWS Support](http://aws.amazon.com/contact-us/)\.

If you don't need to process all of your transcription jobs concurrently, use [Job queuing](job-queuing.md)\. This enables Amazon Transcribe to keep track of your transcription jobs and process them when slots are available\. You can request an increase to the job queue bandwidth ratio to run more transcription jobs\. The quota for the transcription jobs in your job queue is the product of the number of transcription jobs you can run concurrently and the bandwidth ratio\. For example, if you have a bandwidth ratio of `5` and a quota of `100` for the number of transcription jobs you can run concurrently then you can have 500 transcription jobs in your job queue\.

## Quotas<a name="limits"></a>

You can request a quota increase for the following resources:


| Resource | Default | 
| --- | --- | 
| Number of concurrent batch transcription jobs | 250 | 
| Number of concurrent batch transcription jobs \(call analytics\) | 100 | 
| Job queue bandwidth ratio | 0\.9 | 
| Number of concurrent HTTP/2 streams for streaming transcription | 25 | 
| Number of [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md)WebSocket requests | 25 | 
| Total number of vocabularies per account | 100 | 
| Number of pending vocabularies | 10 | 
| Number of concurrently training custom language models | 3 | 
| Total number of custom language models per account | 10 | 
| Number of categories per account \(call analytics\) | 200 | 
| Number of rules per category \(call analytics\) | 20 | 

The following operations limits can also be increased upon request:


| Operation | Transactions per second | 
| --- | --- | 
| [ StartTranscriptionJob ](API_StartTranscriptionJob.md) | 25 | 
| [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) | 25 | 
| [ GetTranscriptionJob ](API_GetTranscriptionJob.md) | 30 | 
| [ DeleteTranscriptionJob ](API_DeleteTranscriptionJob.md) | 5 | 
| [ ListTranscriptionJobs ](API_ListTranscriptionJobs.md) | 5 | 
| [ CreateVocabulary ](API_CreateVocabulary.md) | 10 | 
| [ UpdateVocabulary ](API_UpdateVocabulary.md) | 10 | 
| [ DeleteVocabulary ](API_DeleteVocabulary.md) | 5 | 
| [ GetVocabulary ](API_GetVocabulary.md) | 20 | 
| [ ListVocabularies ](API_ListVocabularies.md) | 5 | 
| [ StartCallAnalyticsJob ](API_StartCallAnalyticsJob.md) | 10 | 
| [ GetCallAnalyticsJob ](API_GetCallAnalyticsJob.md) | 20 | 
| [ ListCallAnalyticsJobs ](API_ListCallAnalyticsJobs.md) | 5 | 
| [ DeleteCallAnalyticsJob ](API_DeleteCallAnalyticsJob.md) | 5 | 
| [ CreateCallAnalyticsCategory ](API_CreateCallAnalyticsCategory.md) | 10 | 
| [ UpdateCallAnalyticsCategory ](API_UpdateCallAnalyticsCategory.md) | 10 | 
| [ DeleteCallAnalyticsCategory ](API_DeleteCallAnalyticsCategory.md) | 5 | 
| [ GetCallAnalyticsCategory ](API_GetCallAnalyticsCategory.md) | 20 | 
| [ ListCallAnalyticsCategories ](API_ListCallAnalyticsCategories.md) | 5 | 

**Note**  
For information about requesting a quota increase, see [AWS Service Quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *Amazon Web Services General Reference*\.

The following quotas **cannot** be changed:


| Description | Quota | 
| --- | --- | 
| Audio file length | 4:00:00 \(four\) hours \(14,400 seconds\) | 
| Audio file size | 2 GB | 
| Audio file size \(call analytics\) | 500 MB | 
| Size of a custom vocabulary | 50 KB | 
| Length of a custom vocabulary phrase | 256 characters | 
| Size of a vocabulary filter | 50 KB | 
| Number of vocabulary filters | 100 | 
| Number of channels for channel identification | 2 | 
| Number of days job records are retained | 90 | 
| Minimum audio file duration | 500 milliseconds \(ms\) | 