# Amazon Transcribe features<a name="feature-matrix"></a>

Amazon Transcribe offers several services that each support a different subset of features\.

In the following table, 'batch' refers to transcribing a file that is located in an Amazon S3 bucket and 'streaming' refers to transcribing media in real time\. For Call Analytics, 'post\-call' refers to transcribing a media file located in an Amazon S3 bucket and 'real\-time' refers to transcribing streamed media in real time\.


| Feature | Amazon Transcribe | [Amazon Transcribe Medical](transcribe-medical.md)1 | [Amazon Transcribe Call Analytics](call-analytics.md) | 
| --- | --- | --- | --- | 
| Configuration options | 
| [Language identification](lang-id.md) \(single\-language audio\) | batch, streaming | N/A | post\-call | 
| [Language identification](lang-id-batch.md#lang-id-batch-multi-language) \(multi\-language audio\) | batch, streaming | N/A | No | 
| [Channel identification](channel-id.md) | batch, streaming | batch, streaming | post\-call, real\-time | 
| [Job queueing](job-queueing.md) | batch | No | post\-call | 
| [Speaker diarization](diarization.md) | batch, streaming | batch, streaming | post\-call | 
| [Transcribing digits](how-numbers.md)2 | batch, streaming | batch, streaming | post\-call, real\-time | 
| Conversation analytics | 
| [Issue detection](call-analytics.md) \(action items, issue detection, outcomes\)2 | No | No | post\-call, real\-time | 
| [Non\-talk time](call-analytics.md) \(silent periods\)2 | No | No | post\-call, real\-time | 
| [Speaker interruptions](call-analytics.md)2 | No | No | post\-call, real\-time | 
| [Speaker sentiment](call-analytics.md)2 | No | No | post\-call, real\-time | 
| [Talk speed](call-analytics.md)2 | No | No | post\-call, real\-time | 
| Language customization | 
| [Custom language models](custom-language-models.md)2 | batch, streaming | No | post\-call, real\-time | 
| [Custom vocabularies](custom-vocabulary.md) | batch, streaming | batch, streaming | post\-call, real\-time | 
| Resource organization | 
| [Tagging](tagging.md) | batch | batch, streaming | No | 
| Sensitive data | 
|  [Identifying personal health information](phi-id.md)2  | No | batch, streaming | No | 
| [Identifying personally identifiable information](pii-redaction-stream.md)2 | streaming | No | real\-time | 
| [Redacting audio](call-analytics-batch.md#tca-pii-redact-batch)2 | No | No | post\-call, real\-time | 
| [Redacting transcripts](pii-redaction.md)2 | batch, streaming | No | post\-call, real\-time | 
| [Vocabulary filtering](vocabulary-filtering.md) | batch, streaming | no | post\-call, real\-time | 
| Video | 
| [Subtitles](subtitles.md) | batch | No | No | 

****  
1 Amazon Transcribe Medical is only available in US English\.  
2 This feature is not available for all languages; review the [Supported languages and language\-specific features](supported-languages.md) table for more details\.