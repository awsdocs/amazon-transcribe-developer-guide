# Identifying PHI in a real\-time stream<a name="phi-id-stream"></a>

You can identify Personally Identifiable Health Information \(PHI\) in either HTTP/2 or WebSocket streams\. When you activate PHI Identification, Amazon Transcribe Medical labels the PHI that it identifies in the transcription results\. For information about the PHI that Amazon Transcribe Medical can identify, see [Identifying personal health information \(PHI\) in a transcription](phi-id.md)\. 



## Identifying PHI in a dictation that is spoken into your microphone<a name="console-stream-phi"></a>

To use the Amazon Transcribe Medical console to transcribe the speech picked up by your microphone and identify any PHI, choose **Dictation** as the audio input type, start the stream, and begin speaking into the microphone on your computer\.

**To identify PHI in a dictation using the Amazon Transcribe Medical console**

1. Sign in to the [ Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. For **Audio input type**, choose **Dictation**\.

1. For **Additional settings**, choose **PHI identification**\.

1. Choose **Start streaming** and speak into the microphone\.

1. Choose **Stop streaming** to end the dictation\.

## Identifying PHI in an HTTP/2 stream<a name="http2-stream-phi"></a>

To start an HTTP/2 stream with PHI Identification activated, use the [ StartMedicalStreamTranscription ](API_streaming_StartMedicalStreamTranscription.md) API and specify the following:
+ For `LanguageCode`, specify the language code for the language spoken in the stream\. For US English, specify `en-US`\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ For `content-identification-type`, specify `PHI`\.

## Identifying PHI in a WebSocket stream<a name="websocket-phi-id"></a>

 To a start a WebSocket stream with PHI Identification activated, use the following format to create a pre\-signed URL\.

```
GET https://transcribestreaming.region.amazonaws.com:8443/medical-stream-transcription-websocket?
language-code=languageCode 
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
&enable-channel-identification=boolean
&specialty=medical-specialty
&content-identification-type=PHI
```

To start a stream with PHI Identification turned on, you must provide the following values:
+ For `LanguageCode`, specify the language code for the language spoken in the stream\. For US English, specify `en-US`\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ For `content-identification-type`, specify `PHI`\.

The following example is an example response to a streaming request with PHI Identification activated\. For brevity, metadata has been removed\.

```
{
    "TranscriptResultStream": {
        "TranscriptEvent": {
            "Transcript": {
                "Results": [
                    {
                        "Alternatives": [
                            {
                                "Transcript": "my name is john doe",
                                "Items": [
                                    {
                                        "Content": "my",
                                        "EndTime": 0.3799375,
                                        "StartTime": 0.0299375,
                                        "Type": "pronunciation"
                                    },
                                    {
                                        "Content": "name",
                                        "EndTime": 0.5899375,
                                        "StartTime": 0.3899375,
                                        "Type": "pronunciation"
                                    },
                                    {
                                        "Content": "is",
                                        "EndTime": 0.7899375,
                                        "StartTime": 0.5999375,
                                        "Type": "pronunciation"
                                    },
                                    {
                                        "Content": "john",
                                        "EndTime": 0.9199375,
                                        "StartTime": 0.7999375,
                                        "Type": "pronunciation"
                                    },
                                    {
                                        "Content": "doe",
                                        "EndTime": 1.0199375,
                                        "StartTime": 0.9299375,
                                        "Type": "pronunciation"
                                    }
                                ],
                                "Entities": [
                                    {
                                        "Content": "john doe",
                                        "Category": "PHI-Personal",
                                        "Type": "Personal",
                                        "StartTime" : 0.7999375,
                                        "EndTime" : 1.0199375,
                                        "Confidence": 0.9989
                                    }
                                }
                            ]
                        ],
                        "EndTime": 1.02,
                        "IsPartial": false,
                        "ResultId": "2db76dc8-d728-11e8-9f8b-f2801f1b9fd1",
                        "StartTime": 0.0199375
                    }
                ]
            }
        }
    }
}
```