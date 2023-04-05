# How Amazon Transcribe works<a name="how-it-works"></a>

Amazon Transcribe uses machine learning models to convert speech to text\.

In addition to the transcribed text, transcripts contains data about the transcribed content, including confidence scores and timestamps for each word or punctuation mark\. To see an output example, refer to the [Data input and output](how-input.md#how-output) section\. For a complete list of features that you can apply to your transcription, refer to the [feature summary](feature-matrix.md)\.

Transcription methods can be separated into two main categories:
+ **Batch transcriptions**: Transcribe media files that have been uploaded into an Amazon S3 bucket\. You can use the [AWS CLI](getting-started-cli.md), [AWS Management Console](getting-started-console.md), and various [AWS SDKs](getting-started-sdk.md) for batch transcriptions\.
+ **Streaming transcriptions**: Transcribe media streams in real time\. You can use the [AWS Management Console](getting-started-console.md), [HTTP/2](streaming-http2.md), [WebSockets](streaming-websocket.md), and various [AWS SDKs](getting-started-sdk.md) for streaming transcriptions\.

Note that feature and language support differs for batch and streaming transcriptions\. For more information, refer to [Amazon Transcribe features](feature-matrix.md) and [Supported languages](supported-languages.md)\.

**Topics**
+ [Data input and output](how-input.md)
+ [Transcribing numbers and punctuation](how-numbers.md)

**API operations to get you started**  
Batch: [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html)  
Streaming: [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartStreamTranscription.html), StartStreamTranscriptionWebSocket