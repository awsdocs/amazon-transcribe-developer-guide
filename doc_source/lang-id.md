# Identifying the dominant languages in your media<a name="lang-id"></a>

Amazon Transcribe is able to automatically identify the languages spoken in your media without you having to specify a language code\.

[Batch language identification](lang-id-batch.md) can identify the dominant language spoken in your media file or, if your media contains multiple languages, it can identify all languages spoken\. To improve language identification accuracy, you can optionally provide a list of two or more languages you think may be present in your media\.

[Streaming language identification](lang-id-stream.md) can identify one language per channel \(a maximum of two channels are supported\)\. Streaming requests must have a minimum of two additional language options included in your request\. Providing language options allows for faster language identification\. The faster Amazon Transcribe is able to identify the language, the less change there is of data loss in the first few seconds of your stream\.

**Important**  
Batch and streaming transcriptions support different languages\. Refer to the **Data input** column in the [supported languages table](supported-languages.md) for details\. Note that Swedish and Vietnamese are not currently supported with language identification\.

To learn about monitoring and events with language identification, refer to [Language identification events](monitoring-events.md#lang-id-event)\.