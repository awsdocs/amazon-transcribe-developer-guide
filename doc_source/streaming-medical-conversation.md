# Transcribing a medical conversation in a real\-time stream<a name="streaming-medical-conversation"></a>

You can transcribe an audio stream of a medical conversation using either the HTTP/2 or [WebSocket ](https://tools.ietf.org/html/rfc6455) protocols\. For information on how to start a stream using the WebSocket protocol, see [Setting up a WebSocket stream](streaming-websocket.md)\. To start an HTTP/2 stream, use the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API\.

You can transcribe streaming audio in the following medical specialties:
+ Cardiology
+ Neurology
+ Oncology
+ Primary Care
+ Urology

Each medical specialty includes many types of procedures and appointments\. Clinicians therefore dictate many different types of notes\. Use the following examples as guidance to help you specify the value of the `specialty` URI parameter of the WebSocket request, or the `Specialty` parameter of the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API:
+ For electrophysiology or echocardiography consultations, choose `CARDIOLOGY`\.
+ For medical oncology, surgical oncology, or radiation oncology consultations, choose `ONCOLOGY`\.
+ For a physician providing a consultation to a patient who had a stroke, either a transient ischemic attack or a cerebrovascular attack, choose `NEUROLOGY`\.
+ For a consultation around urinary incontinence, choose `UROLOGY`\.
+ For yearly checkup or urgent care visits, choose `PRIMARYCARE`\.
+ For inpatient hospitalist visits, choose `PRIMARYCARE`\.
+ For consultations regarding fertility, tubal ligation, IUD insertion, or abortion, choose `PRIMARYCARE`\.

## AWS Management Console<a name="streaming-medical-conversation-console"></a>

**To transcribe a streaming medical conversation \(AWS Management Console\)**

To use the AWS Management Console to transcribe a clinician\-patient dialogue in real\-time stream, choose the option to transcribe a medical conversation, start the stream, and begin speaking into the microphone\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Real\-time transcription**\.

1. Choose **Conversation**\.

1. For **Medical specialty**, choose the clinician's specialty\.

1. Choose **Start streaming**\.

1. Speak into the microphone\.

## Transcribing a medical conversation in an HTTP/2 stream<a name="http2-med-conversation-streaming"></a>

The following is the syntax for the parameters of an HTTP/2 request\.

To transcribe an HTTP/2 stream of a medical conversation, use the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API and specify the following:
+ `LanguageCode` – The language code\. The valid value is `en-US`
+ `MediaEncoding` – The encoding used for the input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ `Specialty` – The specialty of the medical professional\.
+ `Type` – `CONVERSATION`

To improve transcription accuracy of specific terms in a real\-time stream, use a custom vocabulary\. To enable a custom vocabulary, set the value of `VocabularyName` parameter to the name of the custom vocabulary that you want to use\. For more information, see [Improving transcription accuracy with medical custom vocabularies](vocabulary-med.md)\.

To label the speech from different speakers, set the `ShowSpeakerLabel` parameter to `true`\. For more information, see [Enabling speaker partitioning](conversation-diarization-med.md)\.

For more information on setting up an HTTP/2 stream to transcribe a medical conversation, see [Setting up an HTTP/2 stream](streaming-http2.md)\.

## Transcribing a medical conversation in a WebSocket stream<a name="transcribe-medical-conversation-websocket"></a>

You can use a WebSocket request to transcribe a medical conversation\. When you make a WebSocket request, you create a pre\-signed URI\. This URI contains the information needed to set up the audio stream between your application and Amazon Transcribe Medical\. For more information on creating WebSocket requests, see [Setting up a WebSocket stream](streaming-websocket.md)\.

Use the following template to create your pre\-signed URI\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/medical-stream-transcription-websocket
?language-code=languageCode
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request
&X-Amz-Date=20220208T235959Z
&X-Amz-Expires=250
&X-Amz-Security-Token=security-token
&X-Amz-Signature=Signature Version 4 signature 
&X-Amz-SignedHeaders=host
&media-encoding=flac
&sample-rate=16000
&session-id=sessionId
&specialty=medicalSpecialty
&type=CONVERSATION
&vocabulary-name=vocabularyName
&show-speaker-label=boolean
```

To improve transcription accuracy of specific terms in a real\-time stream, use a custom vocabulary\. To enable a custom vocabulary, set the value of `vocabulary-name` to the name of the custom vocabulary that you want to use\. For more information, see [Improving transcription accuracy with medical custom vocabularies](vocabulary-med.md)\.

To label the speech from different speakers, set the `show-speaker-label` parameter in to `true`\. For more information, see [Enabling speaker partitioning](conversation-diarization-med.md)\.

For more information on creating pre\-signed URIs, see [Setting up a WebSocket stream](streaming-websocket.md)\.