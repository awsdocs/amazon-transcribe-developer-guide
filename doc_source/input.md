# Speech Input<a name="input"></a>

To transcribe an audio file, you use a transcription job\. You store the file as an object in an Amazon S3 bucket\. The input file must be: 
+ In FLAC, MP3, MP4, Ogg, WebM, AMR, or WAV file format
+ Less than 4 hours in length or less than 2 GB of audio data

**Note**  
For AMR, Amazon Transcribe supports both Adaptive Multi\-Rate Wideband \(AMR\-WB\) and Adaptive Multi\-Rate Narrowband \(AMR\-NB\) codecs\.  
For the Ogg and WebM file formats, Amazon Transcribe supports the Opus codec\.

Specify the language and format of the input file\. 

For best results: 
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 8000 Hz for telephone audio\.