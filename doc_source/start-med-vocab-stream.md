# Transcribing a real\-time stream using a medical custom vocabulary<a name="start-med-vocab-stream"></a>

To improve transcription accuracy in a real\-time stream, you can use a custom vocabulary using either HTTP/2 or WebSocket streams\. To start an HTTP/2 request, use the [StartMedicalStreamTranscription](API_streaming_StartMedicalStreamTranscription.md) API\. You can use a custom vocabulary in real\-time using either the Amazon Transcribe Medical console, the [StartMedicalStreamTranscription](API_streaming_StartMedicalStreamTranscription.md) API, or by using the WebSocket protocol\.

## Transcribing a dictation that is spoken into your Microphone \(Console\)<a name="streaming-medical-vocabulary-console"></a>

To use the console to transcribe streaming audio of a medical dictation, choose the option to transcribe a medical dictation, start the stream, and begin speaking into the microphone\.

**To transcribe streaming audio of a medical dictation \(console\)**

1. Sign in to AWS Management Console and open the Amazon Transcribe Medical console at [Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Real\-time transcription**\.

1. For **Medical specialty**, choose the medical specialty of the clinician speaking in the stream\.

1. For **Audio input type**, choose either **Conversation** or **Dictation**\.

1. For **Additional settings**, choose **Custom vocabulary**\.

   1. For **Vocabulary selection**, choose the custom vocabulary\.

1. Choose **Start streaming**\.

1. Speak into the microphone\.

## Identifying speakers in an HTTP/2 stream<a name="vocabulary-med-http2"></a>

The following is the syntax for the parameters of an HTTP/2 request\.

```
            
POST /medical-stream-transcription HTTP/2
x-amzn-transcribe-language-code: LanguageCode
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-specialty: Specialty
x-amzn-transcribe-type: Type
x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
x-amzn-transcribe-session-id: SessionId
Content-type: application/json

{
   "AudioStream": { 
      "AudioEvent": { 
         "AudioChunk": blob
      }
   }
}
```

To use a custom vocabulary in an HTTP/2 stream, use the [StartMedicalStreamTranscription](API_streaming_StartMedicalStreamTranscription.md) API and specify the following: 
+ For `LanguageCode`, specify the language code that corresponds to the language in the stream\. The valid value is `en-US`\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ For `Specialty`, specify the medical specialty of the provider\.
+ For `VocabularyName`, specify the name of the custom vocabulary\.

## Identifying speakers in a WebSocket request<a name="vocabulary-websocket"></a>

To identify speakers in WebSocket streams with the API, use the following format to create a pre\-signed URL to start a WebSocket request and set `vocabulary-name` to the name of the custom vocabulary\. 

```
GET https://transcribestreaming.region.amazonaws.com:8443/medical-stream-transcription-websocket
?language-code=languageCode
   &X-Amz-Algorithm=AWS4-HMAC-SHA256
   &X-Amz-Credential=Signature Version 4 credential scope
   &X-Amz-Date=date
   &X-Amz-Expires=time in seconds until expiration
   &X-Amz-Security-Token=security-token
   &X-Amz-Signature=Signature Version 4 signature 
   &X-Amz-SignedHeaders=host
   &media-encoding=mediaEncoding
   &sample-rate=mediaSampleRateHertz
   &session-id=sessionId
   &specialty=medicalSpecialty
   &type=CONVERSATION
   &vocabulary-name=vocabularyName
   &show-speaker-label=boolean
```