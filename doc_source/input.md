# Speech input<a name="input"></a>

Amazon Transcribe can transcribe speech as either a media file or a real\-time stream\. Your input audio must use the encodings and formats described in the following sections\. For a list of supported languages, see [Supported languages and language\-specific features](how-it-works.md#table-language-matrix)\.

## Containers and formats for batch transcription<a name="batch-format"></a>

When you transcribe an audio file or video file using the [ StartTranscriptionJob ](API_StartTranscriptionJob.md) API or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/), make sure that the file is:
+ In FLAC, MP3, MP4, Ogg, WebM, AMR, or WAV file format
+ Less than 4 hours in length and less than 2 GB in size \(500 MB for call analytics jobs\)

**Note**  
For AMR, Amazon Transcribe supports both Adaptive Multi\-Rate Wideband \(AMR\-WB\) and Adaptive Multi\-Rate Narrowband \(AMR\-NB\) codecs\.  
For the Ogg and WebM file formats, Amazon Transcribe supports the Opus codec\.

For best results: 
+ Use a lossless format\. You can choose either FLAC, or WAV with PCM 16\-bit encoding\.
+ Use a sample rate of 8,000 Hz for telephone audio\.

## Audio containers and formats for streaming transcription<a name="streaming-format"></a>

When you transcribe a real\-time stream using the [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) API or a WebSocket request, make sure that your stream is encoded in:
+ PCM 16\-bit signed little endian
+ FLAC
+ OPUS encoded audio in the Ogg container

For best results:
+ Use a lossless format, such as FLAC or PCM encoding\.
+ Use a sample rate of 8,000 Hz for telephone audio\.

For more information on using a WebSocket request to transcribe your streaming audio, see [Using Amazon Transcribe streaming with WebSockets](websocket.md)\.

For a list of supported languages, see [Supported languages and language\-specific features](how-it-works.md#table-language-matrix)\.