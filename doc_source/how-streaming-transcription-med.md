# Streaming transcription overview<a name="how-streaming-transcription-med"></a>

Streaming transcription takes a stream of your audio data and transcribes it in real time\. It uses a bidirectional WebSocket connection so that the results of the transcription are returned to your application while you send more audio to Amazon Transcribe Medical\. You can also use it when you have an audio file that you want to process as it is transcribed\.

Streaming transcription is available in US English \(en\-US\)\. It can produce transcriptions of accented English, spoken by non\-native speakers\. Streaming audio transcription comes with the following features:
+ Transcribe 16 kHz audio in real time\.
+ Transcribe up to 4 hours of audio streams\.
+ Word\-level timestamp in transcripts\.
+ Word\-level confidence in transcripts\.
+ [Number normalization](how-numbers-med.md)\.
+ Punctuation and true casing in transcripts\.
+ Supports both dictation and conversation speech types\.

For more information, see [Establish a bi\-directional connection using the WebSocket protocol](websocket-med.md)\.