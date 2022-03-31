# Amazon Transcribe features<a name="feature-matrix"></a>

Amazon Transcribe offers several services that each support a different subset of features\.

In the following table, 'batch' refers to transcribing a file that is located in an S3 bucket and 'streaming' refers to transcribing media in real time\.


| Feature | Amazon Transcribe | [Amazon Transcribe Medical](transcribe-medical.md)1 | [Amazon Transcribe Call Analytics](call-analytics.md) | 
| --- | --- | --- | --- | 
| Configuration options | 
| [Identifying languages](lang-id.md) | batch, streaming | N/A | batch | 
| [Transcribing multi\-channel audio](channel-id.md) | batch, streaming | batch, streaming | batch | 
| [Job queuing](job-queuing.md) | batch | No | batch | 
| [Speaker diarization](diarization.md) | batch, streaming | batch, streaming | batch | 
| [Transcribing digits](how-numbers.md)2 | batch, streaming | batch, streaming | batch, streaming | 
| Conversation analytics | 
| [Action items](call-analytics-insights.md#call-analytics-insights-summarization)2 | No | No | batch | 
| [Call outcomes](call-analytics-insights.md#call-analytics-insights-summarization)2 | No | No | batch | 
| [Issue detection](call-analytics-insights.md#call-analytics-insights-summarization)2 | No | No | batch | 
| [Non\-talk time \(silence\)](call-analytics-insights.md#call-analytics-insights-characteristics)2 | No | No | batch | 
| [Speaker interruptions](call-analytics-insights.md#call-analytics-insights-characteristics)2 | No | No | batch | 
| [Speaker sentiment](call-analytics-insights.md#call-analytics-insights-sentiment)2 | No | No | batch | 
| [Talk speed](call-analytics-insights.md#call-analytics-insights-characteristics)2 | No | No | batch | 
| Language customization | 
| [Custom language models](custom-language-models.md)2 | batch, streaming | No | batch | 
| [Custom vocabularies](custom-vocabulary.md) | batch, streaming | Yes | batch | 
| Resource organization | 
| [Tagging resources](tagging.md) | batch | batch, streaming | No | 
| Sensitive data | 
|  [Identifying personal health information](phi-id.md)2  | No | batch, streaming | No | 
| [Identifying personally identifiable information](pii-redaction-stream.md)2 | streaming | No | No | 
| [Redacting audio](call-analytics-insights.md#call-analytics-insights-redaction)2 | No | No | batch | 
| [Redacting transcripts](pii-redaction.md)2 | batch, streaming | No | batch | 
| [Vocabulary filtering](vocabulary-filtering.md) | batch, streaming | batch, streaming | batch | 
| Video | 
| [Subtitles](subtitles.md) | batch | No | No | 

****  
1 Amazon Transcribe Medical is only available in US English\.  
2 This feature is not available for all languages; review the [Supported languages](supported-languages.md) table for more details\.