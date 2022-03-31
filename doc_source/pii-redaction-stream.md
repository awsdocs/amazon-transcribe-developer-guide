# Redacting or identifying PII in a real\-time stream<a name="pii-redaction-stream"></a>

When redacting personally identifiable information \(PII\) from a streaming transcription, Amazon Transcribe replaces each identified instance of PII with `[PII]` in your transcript\.

An additional option available for streaming audio is *PII identification*\. When you activate PII Identification, Amazon Transcribe labels the PII in your transcription results under an `Entities` object\. For an output sample, see [Example redacted streaming output](pii-redaction-output.md#pii-redaction-output-stream) and [Example PII identification output](pii-redaction-output.md#pii-redaction-output-id)\.

PII identification and redaction for streaming jobs is performed only upon complete transcription of the audio segments\.

You can start a streaming transcription using the AWS Management Console, WebSocket, or HTTP/2\.

## AWS Management Console<a name="redaction-howto-console-stream"></a>

1. Sign into the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\. Scroll down to **Content removal settings** and expand this field if it is minimized\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/redaction-stream1.png)

1. Toggle on **PII Identification & redaction**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/redaction-stream2.png)

1. Select either **Identification only** or **Identification & redaction**, then select the PII entity types you want to identify or redact in your transcript\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/redaction-stream3.png)

1. You're now ready to transcribe your stream\. Select the **Start streaming** button and begin speaking\. To end your dictation, select **Stop streaming**\.

## WebSocket stream<a name="redaction-howto-websocket"></a>

This example creates a pre\-signed URL that uses either PII Identification or PII redaction in a WebSocket stream\. Line breaks have been added for readability\. For more information on using WebSocket streams with Amazon Transcribe, see [Setting up a WebSocket stream](streaming-websocket.md)\. For more detail on parameters, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

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
&pii-entity-types=NAME,ADDRESS
&content-redaction-type=PII (or &content-identification-type=PII)
```

You cannot use both `content-identification-type` and `content-redaction-type` in the same request\.

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

## HTTP/2 stream<a name="redaction-howto-http2"></a>

This example creates an HTTP/2 request with PII identification or PII redaction enabled\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Setting up an HTTP/2 stream](streaming-http2.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
POST /stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
X-Amz-Target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
Content-Type: application/vnd.amazon.eventstream
X-Amz-Content-Sha256: string
X-Amz-Date: 20220208T235959Z
Authorization: AWS4-HMAC-SHA256 Credential=access-key/20220208/us-west-2/transcribe/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date;x-amz-target;x-amz-security-token, Signature=string
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000      
x-amzn-transcribe-content-identification-type: PII (or x-amzn-transcribe-content-redaction-type: PII)
x-amzn-transcribe-pii-entity-types: NAME,ADDRESS
transfer-encoding: chunked
```

You cannot use both `content-identification-type` and `content-redaction-type` in the same request\.

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

**Note**  
PII redaction for streaming is only supported in these AWS Regions: Asia Pacific \(Seoul\), Asia Pacific \(Sydney\), Asia Pacific \(Tokyo\), Canada \(Central\), EU \(Frankfurt\), EU \(Ireland\), EU \(London\), US East \(N\. Virginia\), US East \(Ohio\), and US West \(Oregon\)\.