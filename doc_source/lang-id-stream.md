# Language identification with streaming transcriptions<a name="lang-id-stream"></a>

Use streaming language identification to identify the dominant language spoken in a media stream\. Amazon Transcribe requires a minimum of three seconds of speech to identify the predominant language\.

Amazon Transcribe can identify the dominant language spoken in two different channels\. In this case, set the [ChannelIdentification](API_Settings.md#transcribe-Type-Settings-ChannelIdentification) parameter to `true` and each channel is transcribed separately\. Note that the default for this parameter is `false` and if you don't change it, only the first channel is transcribed\.

You must provide a minimum of two language codes with streaming language identification, and you can select only one language variant \(locale\) per language per stream\. This means that you cannot select `en-US` and `en-AU` as language options for the same transcription\.

You also have the option to select a preferred language from the set of language codes you provide\. Adding a preferred language helps Amazon Transcribe identify the language in the first few seconds of your stream\.

Unlike batch language identification, streaming language identification can't be combined with other language\-specific Amazon Transcribe features, such as custom vocabularies, custom language models, vocabulary filtering, or redaction\.

**Note**  
PCM is the only supported audio format for streaming language identification\.

For a list of languages supported with streaming transcriptions, see [supported languages](supported-languages.md#table-language-matrix)\.

You can use automatic language identification in a streaming transcription using the **AWS Console**, **HTTP/2**, or **WebSockets**; see the following for examples:

## Console<a name="lang-howto-console-stream"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\. Scroll down to **Language settings** and expand this field if it is minimized\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream1.png)

1. Select **Automatic language identification**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream2.png)

1. Provide a minimum of 2 language codes for your transcription\. Note that you can provide only one variant \(locale\) per language\. For example, you cannot select both `en-US` and `en-AU` as language options for the same transcription\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream3.png)

1. \(Optional\) From the subset of languages you selected in the previous step, you can choose a preferred language for your transcript\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream4.png)

1. You're now ready to transcribe your stream\. Select the **Start streaming** button and begin speaking\.

## HTTP/2<a name="clm-use-howto-http2"></a>

This example creates an HTTP/2 request with language identification enabled\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Using Amazon Transcribe streaming With HTTP/2](how-streaming.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md)\.

```
POST /stream-transcription HTTP/2.0
host: transcribestreaming.region.amazonaws.com
authorization: Generated value
content-type: application/vnd.amazon.eventstream
x-amz-target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
x-amz-content-sha256: STREAMING-AWS4-HMAC-SHA256-EVENTS
x-amz-date: Date
x-amzn-transcribe-identify-language: true
x-amzn-transcribe-language-options: en-US,de-DE
x-amzn-transcribe-preferred-language: en-US
x-amzn-transcribe-media-encoding: pcm
x-amzn-transcribe-sample-rate: 16000
transfer-encoding: chunked
```

Use the following values in your request:
+ **region**: The AWS Region where you are calling Amazon Transcribe\. For a list of valid Regions, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region)\.
+ **authorization**: The Signature Version 4 signature for the request\. To learn more about creating a signature, see [ Signing AWS requests with Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html)\.
+ **date**: The date and time for your request\. Refer to [Handling dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html) for instructions\.
+ **identify\-language**: When set to `true`, Amazon Transcribe automatically identifies the language spoken in your media\.
+ **language\-options**: Use this field if you set `identify-language` to `true`\. You must provide a minimum of two language codes\. Refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) for supported languages\.
+ **preferred\-language**: Optional\. The language code you want Amazon Transcribe to use for your transcript\.
+ **media\-encoding**: The encoding used for your input audio\. The only supported value for this parameter is `pcm`\.
+ **sample\-rate**: The sample rate of the input audio \(in Hertz\)\. We recommend using 8,000 Hz for low\-quality audio and 16,000 Hz \(or higher\) for high\-quality audio\. The sample rate you specify must match that in the audio file\.

## WebSocket stream<a name="redaction-howto-websocket"></a>

This example creates a pre\-signed URL that uses language identification in a WebSocket stream\. For more information on using WebSocket streams with Amazon Transcribe, see [Using Amazon Transcribe streaming with WebSockets](websocket.md)\. For more detail on parameters, see [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md)\.

```
GET wss://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket?identify-language=true
&X-Amz-Algorithm=AWS4-HMAC-SHA256 
&X-Amz-Credential=Signature Version 4 credential scope 
&X-Amz-Date=date
&X-Amz-Expires=time in seconds until expiration
&X-Amz-Security-Token=security-token
&X-Amz-Signature=Signature Version 4 signature 
&X-Amz-SignedHeaders=host 
&identify-language=true
&language-options=en-US,de-DE
&preferred-language=en-US
&media-encoding=pcm 
&sample-rate=16000 
&session-id=sessionId
```

URL parameters:
+ **region**: The AWS Region where you are calling Amazon Transcribe\. For a list of valid Regions, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region)\.
+ **identify\-language**: When set to `true`, Amazon Transcribe automatically identifies the language spoken in your media\.
+ **language\-options**: Use this field if you set `identify-language` to `true`\. You must provide a minimum of two language codes\. Refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) for supported languages\.
+ **preferred\-language**: Optional\. The language code you want Amazon Transcribe to use for your transcript\.
+ **media\-encoding**: The encoding used for the input audio\. The only supported value for this parameter is `pcm`\.
+ **sample\-rate**: The sample rate of the input audio \(in Hertz\)\. We recommend using 8,000 Hz for low\-quality audio and 16,000 Hz \(or higher\) for high\-quality audio\. The sample rate you specify must match that in the audio file\.

Signature Version 4 parameters:
+ **X\-Amz\-Algorithm**: The algorithm to use in the signing process; this must be `AWS4-HMAC-SHA256`\.
+ **X\-Amz\-Credential**: A string, separated by slashes \("/"\), formed by concatenating your access key ID and your credential scope components\. Credential scope includes the date \(YYYYMMDD\), AWS Region, service name, and a special termination string \(aws4\_request\)\.
+ **X\-Amz\-Date**: The date and time your signature is created in the form YYYYMMDD'T'HHMMSS'Z'\.
+ **X\-Amz\-Expires**: The length of time \(in seconds\) until the credentials expire\. The maximum value is 300 seconds\.
+ **X\-Amz\-Security\-Token**: Optional\. A Signature Version 4 token for temporary credentials\. If you specify this parameter, include it in the canonical request\. For more information, see [Requesting temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_request.html)\.
+ **X\-Amz\-Signature**: The Signature Version 4 signature you generated for your request\.
+ **X\-Amz\-SignedHeaders**: The headers that are signed when creating the signature for your request; this must be `host`\.

For additional details on Signature Version 4 elements, refer to the [AWS General Reference](https://docs.aws.amazon.com/general/latest/gr/sigv4_elements.html)\.