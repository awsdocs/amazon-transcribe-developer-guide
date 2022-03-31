# How Amazon Transcribe Medical works<a name="how-it-works-med"></a>

Amazon Transcribe Medical enables you to transcribe individual audio content with medical information into text\.

Transcription methods can be separated into two main categories:
+ Batch transcription jobs: Transcribing media that have been uploaded into an S3 bucket\.
+ Streaming transcriptions: Transcribing media streams in real time\.

Batch transcription jobs can be created with the [AWS CLI](getting-started-cli.md), [AWS Management Console](getting-started-console.md), and various [AWS SDKs](getting-started-sdk.md)\.

Streaming transcriptions can be created with the [AWS Management Console](getting-started-console.md), [HTTP/2](streaming-http2.md), [WebSockets](streaming-websocket.md), and various [AWS SDKs](getting-started-sdk.md)\.

For more information on medical transcriptions with streaming audio, see [Streaming transcription overview](how-streaming-transcription-med.md) and [Establish a bi\-directional connection using the WebSocket protocol](websocket-med.md)\. For more information on batch transcriptions, see [Batch transcription overview](batch-med-transcription.md)\.