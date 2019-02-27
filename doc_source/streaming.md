# Streaming Transcription<a name="streaming"></a>

Amazon Transcribe streaming transcription enables you to send an audio stream and receive a stream of text in real time\. The API makes it easy for developers to add real\-time speech\-to\-text capability to their applications\.

You can use streaming transcription in the following languages:
+ US English \(en\-US\)
+ US Spanish \(es\-US\)

Amazon Transcribe streaming transcription can be used for a variety of purposes\. For example:
+ Streaming transcriptions can generate real\-time subtitles for live broadcast media\.
+ Lawyers can make real\-time annotations on top of streaming transcriptions during courtroom depositions\.
+ Video game chat can be transcribed in real time so that hosts can moderate content or run real\-time analysis\.
+ Streaming transcriptions can provide assistance to the hearing impaired\.

To make it easier to get started, we provide a streaming client that handles retrying the connection when there are transient problems on the network\. You can use this client as a starting point for your own applications\.

**Topics**
+ [Using Amazon Transcribe Streaming](how-streaming.md)
+ [Streaming Retry Client](streaming-client.md)
+ [Using the Retry Client](retry-client-example.md)
+ [Amazon Transcribe Streaming Format](streaming-format.md)