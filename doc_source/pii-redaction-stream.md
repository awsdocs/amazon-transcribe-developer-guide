# Redacting or identifying PII in a real\-time stream<a name="pii-redaction-stream"></a>

When redacting personally identifiable information \(PII\) from a streaming transcription, Amazon Transcribe replaces each identified instance of PII with `[PII]` in your transcript\.

An additional option available for streaming audio is *PII identification*\. When you activate PII Identification, Amazon Transcribe labels the PII in your transcription results under an `Entities` object\. For an output sample, see [Example redacted streaming output](pii-redaction-output.md#pii-redaction-output-stream) and [Example PII identification output](pii-redaction-output.md#pii-redaction-output-id)\.

PII identification and redaction for streaming jobs is performed only upon complete transcription of the audio segments\.

You can start a streaming transcription using the Amazon Transcribe console, WebSocket, or HTTP/2\.

## Console<a name="redaction-howto-console-stream"></a>

To use the Amazon Transcribe console to transcribe and redact PII from live speech, start the stream and begin speaking into the microphone on your computer\.

**To identify PII in a dictation using the Amazon Transcribe console**

1. Sign into the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. For **Additional settings**, choose **PII redaction** \(or **PII identification**\)\.

1. Choose **Start streaming** and speak into the microphone\.

1. Choose **Stop streaming** to end the dictation\.

## WebSocket stream<a name="redaction-howto-websocket"></a>

This example creates a pre\-signed URL that uses wither PII Identification or PII redaction in a WebSocket stream\. For more information on using WebSocket streams with Amazon Transcribe, see [Using Amazon Transcribe streaming with WebSockets](websocket.md)\. For more detail on parameters, see [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md)\.

```
GET wss://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket?language-code=en-US 
&X-Amz-Algorithm=AWS4-HMAC-SHA256 
&X-Amz-Credential=Signature Version 4 credential scope 
&X-Amz-Date=date
&X-Amz-Expires=time in seconds until expiration
&X-Amz-Security-Token=security-token
&X-Amz-Signature=Signature Version 4 signature 
&X-Amz-SignedHeaders=host 
&media-encoding=mediaEncoding 
&sample-rate=16000 
&session-id=sessionId
&enable-channel-identification=true
&number-of-channels=2
&show-speaker-label=true    
&pii-entity-types=NAME,ADDRESS
&content-redaction-type=PII (or &content-identification-type=PII)
```

**Important**  
In the preceding code example, you can only have one of `&content-redaction-type=PII` or `&content-identification-type=PII`, not both\.

URL parameters:
+ **region**: The AWS Region where you are calling Amazon Transcribe\. For a list of valid Regions, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region)\.
+ **language\-code**: The language code for the input audio\. Refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) for supported languages\.
+ **media\-encoding**: The encoding used for the input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **sample\-rate**: The sample rate of the input audio \(in Hertz\)\. We recommend using 8,000 Hz for low\-quality audio and 16,000 Hz \(or higher\) for high\-quality audio\. The sample rate you specify must match that in the audio file\.
+ **session\-id**: Optional\. An identifier for the transcription session\. If you don't provide a session ID, Amazon Transcribe generates one for you and returns it in the response\.
+ **enable\-channel\-identification**: Identify speakers on multiple audio channels; valid values are `true` and `false`\.
+ **number\-of\-channels**: Add the number of audio channels in your stream\. Use this field only if you set `enable-channel-identification` to `true`\.
+ **show\-speaker\-label**: When set to `true`, your speakers are distinguished in your transcript\.
+ **content\-redaction\-type**: Optional\. The value must be `PII`\. Include this field to redact PII in your transcription results\. You can only use this parameter if you **are not** using `content-identification-type`\.
+ **content\-identification\-type**: Optional\. The value must be `PII`\. Include this field to identify PII in your transcription results\. You can only use this parameter if you **are not** using `content-redaction-type`\.
+ **pii\-entity\-types**: Specify the types of PII that you want to identify\. You can specify one or more values\. Note that `pii-entity-types` is an optional parameter with a default of `ALL`; if you don't specify which entities you want to redact \(or identify\), all PII entity types are redacted \(or identified\)\.

  The available values for `pii-entity-types` are: `BANK_ACCOUNT_NUMBER`, `BANK_ROUTING`, `CREDIT_DEBIT_NUMBER`, `CREDIT_DEBIT_CVV`, `CREDIT_DEBIT_EXPIRY`, `PIN`, `EMAIL`, `ADDRESS`, `NAME`, `PHONE`, `SSN`, or `ALL`

Signature Version 4 parameters:
+ **X\-Amz\-Algorithm**: The algorithm to use in the signing process; this must be `AWS4-HMAC-SHA256`\.
+ **X\-Amz\-Credential**: A string, separated by slashes \("/"\), formed by concatenating your access key ID and your credential scope components\. Credential scope includes the date \(YYYYMMDD\), AWS Region, service name, and a special termination string \(aws4\_request\)\.
+ **X\-Amz\-Date**: The date and time your signature is created in the form YYYYMMDD'T'HHMMSS'Z'\.
+ **X\-Amz\-Expires**: The length of time \(in seconds\) until the credentials expire\. The maximum value is 300 seconds\.
+ **X\-Amz\-Security\-Token**: Optional\. A Signature Version 4 token for temporary credentials\. If you specify this parameter, include it in the canonical request\. For more information, see [Requesting temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_request.html)\.
+ **X\-Amz\-Signature**: The Signature Version 4 signature you generated for your request\.
+ **X\-Amz\-SignedHeaders**: The headers that are signed when creating the signature for your request; this must be `host`\.

For additional details on Signature Version 4 elements, refer to the [AWS General Reference](https://docs.aws.amazon.com/general/latest/gr/sigv4_elements.html)\.

## HTTP/2 stream<a name="redaction-howto-http2"></a>

This example creates an HTTP/2 request with PII identification or PII redaction enabled\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Using Amazon Transcribe streaming With HTTP/2](how-streaming.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md)\.

```
POST /stream-transcription HTTP/2
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-sample-rate: 16000
x-amzn-transcribe-session-id: SessionId
x-amzn-transcribe-enable-channel-identification: true
x-amzn-transcribe-number-of-channels: 2
x-amzn-transcribe-show-speaker-label: true
x-amzn-transcribe-content-identification-type: PII (or x-amzn-transcribe-content-redaction-type: PII)
x-amzn-transcribe-pii-entity-types: NAME,ADDRESS
Content-type: application/json
```

Use the following values in your request:
+ **language\-code**: The language code for the language spoken in the stream\. For US English, specify `en-US`\.
+ **media\-encoding**: The encoding used for the input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **sample\-rate**: The sample rate of the audio in Hz\.
+ **session\-id**: Optional\. An identifier for the transcription session\. If you don't provide a session ID, Amazon Transcribe generates one for you and returns it in the response\.
+ **enable\-channel\-identification**: Identify speakers on multiple audio channels; valid values are `true` and `false`\.
+ **number\-of\-channels**: Add the number of audio channels in your stream\. Use this field only if you set `enable-channel-identification` to `true`\.
+ **show\-speaker\-label**: When set to `true`, your speakers are distinguished in your transcript\.
+ **content\-redaction\-type**: Optional\. The value must be `PII`\. Include this field to redact PII in your transcription results\. You can only use this parameter if you **are not** using `content-identification-type`\.
+ **content\-identification\-type**: Optional\. The value must be `PII`\. Include this field to identify PII in your transcription results\. You can only use this parameter if you **are not** using `content-redaction-type`\.
+ **pii\-entity\-types**, specify the types of PII you want to identify\. You can specify one or more values\. `pii-entity-types` is an optional parameter with a default of `ALL`; if you don't specify which entities you want to redact \(or identify\), all PII entity types are redacted \(or identified\)\.

  The available values for `PiiEntityTypes` are: `BANK_ACCOUNT_NUMBER`, `BANK_ROUTING`, `CREDIT_DEBIT_NUMBER`, `CREDIT_DEBIT_CVV`, `CREDIT_DEBIT_EXPIRY`, `PIN`, `EMAIL`, `ADDRESS`, `NAME`, `PHONE`, `SSN`, and `ALL`\. `PiiEntityTypes` is an optional parameter with a default value of `ALL`\.

**Note**  
PII redaction for streaming is only supported in these AWS Regions: Asia Pacific \(Seoul\), Asia Pacific \(Sydney\), Asia Pacific \(Tokyo\), Canada \(Central\), EU \(Frankfurt\), EU \(Ireland\), EU \(London\), US East \(N\. Virginia\), US East \(Ohio\), and US West \(Oregon\)\.