# How Amazon Transcribe works<a name="how-it-works"></a>

Amazon Transcribe analyzes media that contains speech and uses advanced machine learning techniques to transcribe the voice data into text\. You can then use the transcription as you would any text document\.

Transcription methods can be separated into two main categories:
+ Batch transcription jobs: Transcribing media that have been uploaded into an S3 bucket\.
+ Streaming transcriptions: Transcribing media streams in real time\.

Batch transcription jobs can be created with the [AWS CLI](getting-started-cli.md), [AWS Management Console](getting-started-console.md), and various [AWS SDKs](getting-started-sdk.md)\.

Streaming transcriptions can be created with the [AWS Management Console](getting-started-console.md), [HTTP/2](streaming-http2.md), [WebSockets](streaming-websocket.md), and various [AWS SDKs](getting-started-sdk.md)\.

For information on supported file containers and formats for both batch and streaming options, see [Data input and output](how-input.md)\.

**API operations to get you started**  
Batch: [GetTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetTranscriptionJob.html), [ListTranscriptionJobs](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListTranscriptionJobs.html), [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html)  
Streaming: [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartStreamTranscription.html) 