# Transcribing a real\-time stream using a medical custom vocabulary<a name="start-med-vocab-stream"></a>

To improve transcription accuracy in a real\-time stream, you can use a custom vocabulary using either HTTP/2 or WebSocket streams\. To start an HTTP/2 request, use the [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API\. You can use a custom vocabulary in real\-time using either the AWS Management Console, the [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API, or by using the WebSocket protocol\.

## Transcribing a dictation that is spoken into your Microphone \(AWS Management Console\)<a name="streaming-medical-vocabulary-console"></a>

To use the AWS Management Console to transcribe streaming audio of a medical dictation, choose the option to transcribe a medical dictation, start the stream, and begin speaking into the microphone\.

**To transcribe streaming audio of a medical dictation \(AWS Management Console\)**

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Real\-time transcription**\.

1. For **Medical specialty**, choose the medical specialty of the clinician speaking in the stream\.

1. For **Audio input type**, choose either **Conversation** or **Dictation**\.

1. For **Additional settings**, choose **Custom vocabulary**\.

   1. For **Vocabulary selection**, choose the custom vocabulary\.

1. Choose **Start streaming**\.

1. Speak into the microphone\.

## Enabling speaker partitioning in an HTTP/2 stream<a name="vocabulary-med-http2"></a>

The following is the syntax for the parameters of an HTTP/2 request\.

```
POST /medical-stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
authorization: Generated value
x-amz-target: com.amazonaws.transcribe.Transcribe.StartMedicalStreamTranscription
x-amz-content-sha256: STREAMING-MED-AWS4-HMAC-SHA256-EVENTS
x-amz-date: 20220208T235959Z
x-amzn-transcribe-session-id: my-first-http2-med-stream
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000
x-amzn-transcribe-vocabulary-name: my-first-med-vocab
x-amzn-transcribe-specialty: PRIMARYCARE
x-amzn-transcribe-type: CONVERSATION
x-amzn-transcribe-show-speaker-label: true
Content-type: application/vnd.amazon.eventstream
transfer-encoding: chunked
```

Parameter descriptions:
+ **host**: Update the AWS Region \('us\-west\-2' in the preceding example\) with the AWS Region you are calling\. For a list of valid AWS Regions, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region)\.
+ **authorization**: This is a generated field\. To learn more about creating a signature, see [Signing AWS requests with Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html)\.
+ **x\-amz\-target**: Don't alter this field; use the content shown in the preceding example\.
+ **x\-amz\-content\-sha256**: This is a generated field\. To learn more about calculating a signature, see [Signing AWS requests with Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html)\.
+ **x\-amz\-date**: The date and time the signature is created\. The format is YYYYMMDDTHHMMSSZ, where YYYY=year, MM=month, DD=day, HH=hour, MM=minute, SS=seconds, and 'T' and 'Z' are fixed characters\. For more information, refer to [Handling Dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html)\.
+ **x\-amzn\-transcribe\-session\-id**: The name for your streaming session\.
+ **x\-amzn\-transcribe\-language\-code**: The encoding used for your input audio\. Refer to [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) or [Supported languages and language\-specific features](supported-languages.md) for a list of valid values\.
+ **x\-amzn\-transcribe\-media\-encoding**: The encoding used for your input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **x\-amzn\-transcribe\-sample\-rate**: The sample rate of the input audio \(in Hertz\)\. Amazon Transcribe supports a range from 8,000 Hz to 48,000 Hz\. Low\-quality audio, such as telephone audio, is typically around 8,000 Hz\. High\-quality audio typically ranges from 16,000 Hz to 48,000 Hz\. Note that the sample rate you specify **must** match that of your audio\.
+ **x\-amzn\-transcribe\-vocabulary\-name**: The name of the vocabulary you want to use with your transcription\.
+ **x\-amzn\-transcribe\-specialty**: The medical specialty being transcribed\.
+ **x\-amzn\-transcribe\-type**: Choose whether this is a dictation or a conversation\.
+ **x\-amzn\-transcribe\-show\-speaker\-label**: To enable diarization, this value must be `true`\.
+ **content\-type**: Don't alter this field; use the content shown in the preceding example\.

## Enabling speaker partitioning in a WebSocket request<a name="vocabulary-websocket"></a>

To partition speakers in WebSocket streams with the API, use the following format to create a pre\-signed URI to start a WebSocket request and set `vocabulary-name` to the name of the custom vocabulary\. 

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/medical-stream-transcription-websocket
?language-code=en-US
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