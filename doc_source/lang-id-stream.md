# Language identification with streaming transcriptions<a name="lang-id-stream"></a>

Use streaming language identification to identify the dominant language spoken in a media stream\. Amazon Transcribe requires a minimum of three seconds of speech to identify the predominant language\.

Amazon Transcribe can identify the dominant language spoken in two different channels\. In this case, set the [ChannelIdentification](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Settings.html#transcribe-Type-Settings-ChannelIdentification) parameter to `true` and each channel is transcribed separately\. Note that the default for this parameter is `false` and if you don't change it, only the first channel is transcribed\.

You must provide a minimum of two language codes with streaming language identification, and you can select only one language variant \(locale\) per language per stream\. This means that you cannot select `en-US` and `en-AU` as language options for the same transcription\.

You also have the option to select a preferred language from the set of language codes you provide\. Adding a preferred language helps Amazon Transcribe identify the language in the first few seconds of your stream\.

Streaming language identification can't be combined with custom language models or redaction\.

**Note**  
PCM and FLAC are the only supported audio formats for streaming language identification\.

For a list of languages supported with streaming transcriptions, see [supported languages](supported-languages.md#table-language-matrix)\.

You can use automatic language identification in a streaming transcription using the **AWS Management Console**, **HTTP/2**, or **WebSockets**; see the following for examples:

## AWS Management Console<a name="lang-howto-console-stream"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\. Scroll down to **Language settings** and expand this field if it is minimized\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream1.png)

1. Select **Automatic language identification**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream2.png)

1. Provide a minimum of 2 language codes for your transcription\. Note that you can provide only one variant \(locale\) per language\. For example, you cannot select both `en-US` and `en-AU` as language options for the same transcription\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream3.png)

1. \(Optional\) From the subset of languages you selected in the previous step, you can choose a preferred language for your transcript\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/lang-id-stream4.png)

1. You're now ready to transcribe your stream\. Select the **Start streaming** button and begin speaking\. To end your dictation, select **Stop streaming**\.

## HTTP/2<a name="lang-id-howto-http2"></a>

This example creates an HTTP/2 request with language identification enabled\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Setting up an HTTP/2 stream](streaming-http2.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
POST /stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
X-Amz-Target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
Content-Type: application/vnd.amazon.eventstream
X-Amz-Content-Sha256: string
X-Amz-Date: 20220208T235959Z
Authorization: AWS4-HMAC-SHA256 Credential=access-key/20220208/us-west-2/transcribe/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date;x-amz-target;x-amz-security-token, Signature=string
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000    
x-amzn-transcribe-identify-language: true
x-amzn-transcribe-language-options: en-US,de-DE
x-amzn-transcribe-preferred-language: en-US
transfer-encoding: chunked
```

If you use `identify-language` in your request, you must also include `language-options`\. You cannot use both `language-code` and `identify-language` in the same request\.

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

## WebSocket stream<a name="lang-id-howto-websocket"></a>

This example creates a pre\-signed URL that uses language identification in a WebSocket stream\. Line breaks have been added for readability\. For more information on using WebSocket streams with Amazon Transcribe, see [Setting up a WebSocket stream](streaming-websocket.md)\. For more detail on parameters, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/stream-transcription-websocket?
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request
&X-Amz-Date=20220208T235959Z
&X-Amz-Expires=250
&X-Amz-Security-Token=security-token
&X-Amz-Signature=string
&X-Amz-SignedHeaders=content-type%3Bhost%3Bx-amz-date
&language-code=en-US
&media-encoding=flac
&sample-rate=16000
&identify-language=true
&language-options=en-US,de-DE
&preferred-language=en-US
```

If you use `identify-language` in your request, you must also include `language-options`\. You cannot use both `language-code` and `identify-language` in the same request\.

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.