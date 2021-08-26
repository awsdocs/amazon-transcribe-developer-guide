# Transcribing a medical dictation in a real\-time stream<a name="streaming-medical-dictation"></a>

Use a WebSocket stream to transcribe a medical dictation as an audio stream\. You can also use the Amazon Transcribe Medical console to transcribe speech that you or others speak directly into a microphone\.

 For an HTTP/2 or a WebSocket stream, you can transcribe audio in the following medical specialties: 
+ Cardiology
+ Oncology
+ Neurology
+ Primary Care
+ Radiology
+ Urology

Each medical specialty includes many types of procedures and appointments\. Clinicians therefore dictate many different types of notes\. Use the following examples as guidance to help you specify the value of the `specialty` URL parameter of the WebSocket request, or the `Specialty` parameter of the [StartMedicalStreamTranscription](API_streaming_StartMedicalStreamTranscription.md) API:
+ For a dictation after electrophysiology or echocardiogram procedure, choose `CARDIOLOGY`\.
+ For a dictation after a surgical oncology or radiation oncology procedure, choose `ONCOLOGY`\.
+ For a physician dictating notes indicating a diagnosis of encephalitis, choose `NEUROLOGY`\.
+ For a dictation of procedure notes to break up a bladder stone, choose `UROLOGY`\.
+ For a dictation of clinician notes after an internal medicine consultation, choose `PRIMARYCARE`\.
+ For a dictation of a physician communicating the findings of a CT scan, PET scan, MRI, or radiograph, choose `RADIOLOGY`\.
+ For a dictation of physician notes after a gynecology consultation, choose `PRIMARYCARE`\.

To improve transcription accuracy of specific terms in a real\-time stream, use a custom vocabulary\. To enable a custom vocabulary, set the value of `vocabulary-name` to the name of the custom vocabulary you want to use\.

## Transcribing a dictation spoken into your microphone with the console<a name="streaming-medical-dictation-console"></a>

To use the console to transcribe streaming audio of a medical dictation, choose the option to transcribe a medical dictation, start the stream, and begin speaking into the microphone\.

**To transcribe streaming audio of a medical dictation \(console\)**

1. Sign in to the [ Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Real\-time transcription**\.

1. Choose **Dictation**\.

1. For **Medical specialty**, choose the medical specialty of the clinician speaking in the stream\.

1. Choose **Start streaming**\.

1. Speak into the microphone\.

## Transcribing a dictation in an HTTP/2 stream<a name="http2-med-dictation-streaming"></a>

To transcribe an HTTP/2 stream of a medical dictation, use the [StartMedicalStreamTranscription](API_streaming_StartMedicalStreamTranscription.md) API and specify the following:
+ `LanguageCode` – The language code\. The valid value is `en-US`
+ `MediaEncoding` – The encoding used for the input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ `Specialty` – The specialty of the medical professional\.
+ `Type` – `DICTATION`

For more information on setting up an HTTP/2 stream to transcribe a medical dictation, see [Streaming request](how-streaming-med.md#streaming-med-request)\.

## Using a WebSocket streaming request to transcribe a medical dictation<a name="transcribe-medical-dictation-websocket"></a>

To transcribe a medical dictation in a real\-time stream using a WebSocket request, you create a pre\-signed URL\. This URL contains the information needed to set up the audio stream between your application and Amazon Transcribe Medical\. For more information on creating WebSocket requests, see [Establish a bi\-directional connection using the WebSocket protocol](websocket-med.md)\.

Use the following template to create your pre\-signed URL\.

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
   &type=DICTATION
   &vocabulary-name=vocabularyName
   &show-speaker-label=boolean
```

For more information on creating pre\-signed URLs, see [Creating a pre\-signed URL](websocket-med.md#websocket-url-med)\.