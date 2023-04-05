# Amazon Transcribe features<a name="feature-matrix"></a>

To help you decide which Amazon Transcribe solution best fits your use case, the following table offers a feature comparison\.

Note that 'batch' and 'post\-call' refer to transcribing a file that is located in an Amazon S3 bucket and 'streaming' and 'real\-time' refer to transcribing media in real time\.


| Feature | Amazon Transcribe | [Amazon Transcribe Medical](transcribe-medical.md)1 | [Amazon Transcribe Call Analytics](call-analytics.md) | 
| --- | --- | --- | --- | 
| Configuration options | 
| [Language identification](lang-id.md) \(single\-language audio\) | batch, streaming | N/A | post\-call | 
| [Language identification](lang-id-batch.md#lang-id-batch-multi-language) \(multi\-language audio\) | batch, streaming | N/A | no | 
| [Channel identification](channel-id.md) | batch, streaming | batch, streaming | post\-call, real\-time | 
| [Job queueing](job-queueing.md) | batch | no | post\-call | 
| [Speaker diarization](diarization.md) | batch, streaming | batch, streaming | post\-call | 
| [Alternative transcriptions](alternatives.md) | batch, streaming | batch, streaming | no | 
| [Transcribing digits](how-numbers.md)2 | batch, streaming | batch, streaming | post\-call, real\-time | 
| Conversation analytics | 
| [Issue detection](call-analytics.md) \(action items, issue detection, outcomes\)2 | no | no | post\-call, real\-time | 
| [Non\-talk time](call-analytics.md) \(silent periods\)2 | no | no | post\-call, real\-time | 
| [Speaker interruptions](call-analytics.md)2 | no | no | post\-call, real\-time | 
| [Speaker sentiment](call-analytics.md)2 | no | no | post\-call, real\-time | 
| [Talk speed](call-analytics.md)2 | no | no | post\-call, real\-time | 
| Language customization | 
| [Custom language models](custom-language-models.md)2 | batch, streaming | no | post\-call, real\-time | 
| [Custom vocabularies](custom-vocabulary.md) | batch, streaming | batch, streaming | post\-call, real\-time | 
| Resource organization | 
| [Tagging](tagging.md) | batch | batch, streaming | no | 
| Sensitive data | 
|  [Identifying personal health information](phi-id.md)2  | no | batch, streaming | no | 
| [Identifying personally identifiable information](pii-redaction-stream.md)2 | streaming | no | real\-time | 
| [Redacting audio](call-analytics-batch.md#tca-pii-redact-batch)2 | no | no | post\-call, real\-time | 
| [Redacting transcripts](pii-redaction.md)2 | batch, streaming | no | post\-call, real\-time | 
| [Vocabulary filtering](vocabulary-filtering.md) | batch, streaming | no | post\-call, real\-time | 
| Video | 
| [Subtitles](subtitles.md) | batch | no | no | 

****  
1 Amazon Transcribe Medical is only available in US English\.  
2 This feature is not available for all languages; review the [Supported languages and language\-specific features](supported-languages.md) table for more details\.