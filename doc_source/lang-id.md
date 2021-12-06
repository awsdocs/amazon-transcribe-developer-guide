# Identifying the dominant language in your media files<a name="lang-id"></a>

Amazon Transcribe is able to automatically identify the language spoken in a media file without you having to specify a language code\. Language identification works for all [supported languages](supported-languages.md#table-language-matrix); note that supported languages differ for batch jobs and streaming transcriptions\.

Batch jobs can only be transcribed in one language, while streaming transcriptions can have one language per channel \(a maximum of two channels are supported\)\.

To improve language identification accuracy, you can provide a list of languages you think may be present\. From this list, Amazon Transcribe chooses the closest matching language to transcribe your audio\. Providing language codes is optional with batch jobs and required for streaming transcriptions\. If none of the language codes you provide match languages spoken in your media, your transcription accuracy is diminished\.

**Note**  
If none of your selected languages codes match any of the languages spoken in your media, Amazon Transcribe selects the closest option in your subset of selected language codes and produces a transcript based on that language\. For example, if your media is in US English \(`en-US`\) and you provide Amazon Transcribe with the language codes `zh-CN`, `fr-FR`, and `de-DE`, Amazon Transcribe is likely to match your media to German \(`de-DE`\) and produce a German\-language transcription\. Mismatching language codes and spoken languages can result in a very inaccurate transcript, so we advise caution when selecting language codes\.

For additional information, see [Language identification with batch transcription jobs](lang-id-batch.md) and [Language identification with streaming transcriptions](lang-id-stream.md)\.

To learn about monitoring and events with language identification, refer to [Language identification events](cloud-watch-events.md#lang-id-event)\.