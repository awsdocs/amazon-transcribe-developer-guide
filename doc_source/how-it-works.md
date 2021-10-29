# How Amazon Transcribe works<a name="how-it-works"></a>

Amazon Transcribe analyzes audio files that contain speech and uses advanced machine learning techniques to transcribe the voice data into text\. You can then use the transcription as you would any text document\.

Each language has its own language code, listed in the [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) table, that you can use to specify the language of your audio or video file\.

You can transcribe an uploaded file or live\-stream audio\. Processing an uploaded file is referred to as a **batch transcription job**, while using live audio is referred to as a **streaming transcription**\. For information on supported file containers and formats for both batch and streaming options, see [Speech input](input.md)\.

**API operations to get you started**  
Batch: [GetTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/dg/API_GetTranscriptionJob.html), [ListTranscriptionJobs](https://docs.aws.amazon.com/transcribe/latest/dg/API_ListTranscriptionJobs.html), [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/dg/API_StartTranscriptionJob.html)  
Streaming: [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/dg/API_StartStreamTranscription.html) 