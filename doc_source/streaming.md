# Transcribing streaming audio<a name="streaming"></a>

Using Amazon Transcribe streaming, you can produce real\-time transcriptions for your media content\. Unlike batch transcriptions, which involve uploading media files, streaming media is delivered to Amazon Transcribe in real time\. Amazon Transcribe then returns a transcript, also in real time\.

Streaming can include pre\-recorded media \(movies, music, and podcasts\) and real\-time media \(live news broadcasts\)\. Common streaming use cases for Amazon Transcribe include live closed captioning for sporting events and real\-time monitoring of call center audio\.

Streaming content is delivered as a series of sequential data packets, or 'chunks,' that Amazon Transcribe transcribes instantaneously\. The advantages of using streaming over batch include real\-time speech\-to\-text capabilities in your applications and faster transcription times\. However, this increased speed may have accuracy limitations in some cases\.

Amazon Transcribe offers the following options for streaming:
+ [AWS SDKs](http://aws.amazon.com/developer/tools/) \(see also [Supported programming languages](supported-languages.md#supported-sdks)\)
+ [HTTP/2](streaming-http2.md)
+ [WebSockets](streaming-websocket.md)
+ [AWS Management Console](https://console.aws.amazon.com/transcribe/)

**Tip**  
We strongly recommend using an SDK rather than using HTTP/2 or WebSockets directly\. For SDK code examples, refer to the [AWS Samples repository](https://github.com/orgs/aws-samples/repositories?language=&q=transcribe&sort=&type=all) on GitHub\.

Audio formats supported for streaming transcriptions are:
+ FLAC
+ OPUS\-encoded audio in an Ogg container
+ PCM \(only signed 16\-bit little\-endian audio formats, which does **not** include WAV\)

Lossless formats \(FLAC or PCM\) are recommended\.

To transcribe streaming audio in the AWS Management Console, speak into your computer microphone\.

**Note**  
Streaming transcriptions are not supported with all languages\. Refer to the 'Data input' column in the [supported languages table](supported-languages.md) for details\.

To view the Amazon Transcribe Region availability for streaming transcriptions, see: [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region)\.

**Topics**
+ [Streaming and partial results](streaming-partial-results.md)
+ [Setting up a streaming transcription](streaming-setting-up.md)