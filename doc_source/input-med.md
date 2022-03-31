# Speech input<a name="input-med"></a>

Amazon Transcribe Medical can transcribe speech as either an audio file or a real\-time stream\. Your input audio must use the encodings and formats described in the following sections\.

**Topics**
+ [Containers and formats for batch transcription](#file-format)
+ [Audio containers and formats for streaming transcription](#streaming-format)

## Containers and formats for batch transcription<a name="file-format"></a>

When you transcribe audio using the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API or the AWS Management Console, make sure that the file is:
+ In FLAC, MP3, MP4, Ogg, WebM, AMR, or WAV file format
+ Less than 4 hours in length and less than 2 GB in size
+ Encoded at a sample rate of 16,000 Hz or higher

**Note**  
For AMR, Amazon Transcribe Medical supports both Adaptive Multi\-Rate Wideband \(AMR\-WB\) and Adaptive Multi\-Rate Narrowband \(AMR\-NB\) codecs\.  
For the Ogg and WebM file formats, Amazon Transcribe Medical supports the Opus codec\.

For best results: 
+ Use a lossless format\. You can choose either FLAC, or WAV with PCM 16\-bit encoding\.

## Audio containers and formats for streaming transcription<a name="streaming-format"></a>

When you transcribe a real\-time stream using the [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API or a WebSocket request, make sure that your stream is encoded in:
+ PCM signed 16\-bit little\-endian
+ FLAC
+ OPUS encoded audio in the Ogg container

Your stream must use a sample rate of 16,000 Hz or higher\.

For best results:
+ Use a lossless format, such as FLAC or PCM encoding\.

For more information on using a WebSocket request to transcribe your streaming audio, see [Establish a bi\-directional connection using the WebSocket protocol](websocket-med.md)\.