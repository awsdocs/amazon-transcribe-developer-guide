# How Amazon Transcribe works<a name="how-it-works"></a>

Amazon Transcribe converts speech to text\. A basic transcription request produces a transcript that contains data about the transcribed content, including confidence scores and timestamps for each word or punctuation mark\. For a complete list of features that you can apply to your transcription, refer to the [feature summary](feature-matrix.md)\.

Transcription methods can be separated into two main categories:
+ **Batch transcription jobs**: Transcribe media files that have been uploaded into an Amazon S3 bucket\.
+ **Streaming transcriptions**: Transcribe media streams in real time\.

You can create batch transcriptions using the [AWS CLI](getting-started-cli.md), [AWS Management Console](getting-started-console.md), and various [AWS SDKs](getting-started-sdk.md)\.

You can create streaming transcriptions using the [AWS Management Console](getting-started-console.md), [HTTP/2](streaming-http2.md), [WebSockets](streaming-websocket.md), and various [AWS SDKs](getting-started-sdk.md)\.



**Topics**
+ [Data input and output](how-input.md)
+ [Transcribing numbers and punctuation](how-numbers.md)



**API operations to get you started**  
Batch: [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html)  
Streaming: [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartStreamTranscription.html) 