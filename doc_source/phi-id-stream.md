# Identifying PHI in a real\-time stream<a name="phi-id-stream"></a>

You can identify Personal Health Information \(PHI\) in either HTTP/2 or WebSocket streams\. When you activate PHI Identification, Amazon Transcribe Medical labels the PHI that it identifies in the transcription results\. For information about the PHI that Amazon Transcribe Medical can identify, see [Identifying personal health information \(PHI\) in a transcription](phi-id.md)\. 



## Identifying PHI in a dictation that is spoken into your microphone<a name="console-stream-phi"></a>

To use the AWS Management Console to transcribe the speech picked up by your microphone and identify any PHI, choose **Dictation** as the audio input type, start the stream, and begin speaking into the microphone on your computer\.

**To identify PHI in a dictation using the AWS Management Console**

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. For **Audio input type**, choose **Dictation**\.

1. For **Additional settings**, choose **PHI identification**\.

1. Choose **Start streaming** and speak into the microphone\.

1. Choose **Stop streaming** to end the dictation\.

## Identifying PHI in an HTTP/2 stream<a name="http2-stream-phi"></a>

To start an HTTP/2 stream with PHI Identification activated, use the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API and specify the following:
+ For `LanguageCode`, specify the language code for the language spoken in the stream\. For US English, specify `en-US`\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ For `content-identification-type`, specify `PHI`\.

## Identifying PHI in a WebSocket stream<a name="websocket-phi-id"></a>

 To a start a WebSocket stream with PHI Identification activated, use the following format to create a pre\-signed URL\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/medical-stream-transcription-websocket?
&X-Amz-Algorithm=AWS4-HMAC-SHA256 
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request 
&X-Amz-Date=20220208T235959Z 
&X-Amz-Expires=250 
&X-Amz-Security-Token=security-token 
&X-Amz-Signature=Signature Version 4 signature 
&X-Amz-SignedHeaders=host 
&language-code=en-US
&media-encoding=flac 
&sample-rate=16000 
&specialty=medical-specialty
&content-identification-type=PHI
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.