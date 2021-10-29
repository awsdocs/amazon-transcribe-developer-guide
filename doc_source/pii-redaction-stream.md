# Redacting or identifying PII in a real\-time stream<a name="pii-redaction-stream"></a>

When redacting personally identifiable information \(PII\) from a streaming transcription, Amazon Transcribe replaces each identified instance of PII with `[PII]` in your transcript\.

An additional option available for streaming audio is *PII identification*\. When you activate PII Identification, Amazon Transcribe labels the PII in your transcription results under an `Entities` object\. For an output sample, see [Example redacted streaming output](pii-redaction-output.md#pii-redaction-output-stream) and [Example PII identification output](pii-redaction-output.md#pii-redaction-output-id)\.

PII identification and redaction for streaming jobs is performed only upon complete transcription of the audio segments\.

You can start a streaming transcription using the Amazon Transcribe console, Websocket, or HTTP/2\.

## Console<a name="redaction-howto-console-stream"></a>

To use the Amazon Transcribe console to transcribe and redact PII from live speech, start the stream and begin speaking into the microphone on your computer\.

**To identify PII in a dictation using the Amazon Transcribe console**

1. Sign into the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. For **Additional settings**, choose **PII redaction** \(or **PII identification**\)\.

1. Choose **Start streaming** and speak into the microphone\.

1. Choose **Stop streaming** to end the dictation\.

## WebSocket stream<a name="redaction-howto-websocket"></a>

 To a start a WebSocket stream with PII Identification or PII redaction activated, use the following format to create a pre\-signed URL\.

```
wss://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket?
language-code=en-US 
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
&pii-entity-types=NAME,ADDRESS
&content-redaction-type=PII (or &content-identification-type=PII)
```

**Important**  
In the above code example, you can only have one of `&content-redaction-type=PII` or `&content-identification-type=PII`, not both\.

To start a stream with PII Identification or PII redaction turned on, you must provide the following values:
+ For `LanguageCode`, specify the language code for the language spoken in the stream\. For US English, specify `en-US`; language codes are listed on the [What is Amazon Transcribe?](transcribe-whatis.md) page\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ For `content-identification-type`, specify `PII`\.
+ For `pii-entity-types`, specify the types of PII that you want to identify\. You can specify one or more values\. Note that `pii-entity-types` is an optional parameter with a default of `ALL`; if you don't specify which entities you want to redact \(or identify\), all PII entity types are redacted \(or identified\)\.
+ The available values for `pii-entity-types` are: `BANK_ACCOUNT_NUMBER`, `BANK_ROUTING`, `CREDIT_DEBIT_NUMBER`, `CREDIT_DEBIT_CVV`, `CREDIT_DEBIT_EXPIRY`, `PIN`, `EMAIL`, `ADDRESS`, `NAME`, `PHONE`, `SSN`, or `ALL`

## HTTP/2 stream<a name="redaction-howto-http2"></a>

The following is the syntax for the parameters of an HTTP/2 request with PII identification or PII redaction activated\.

```
POST /stream-transcription HTTP/2
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-session-id: SessionId
x-amzn-transcribe-vocabulary-filter-name: VocabularyFilterName
x-amzn-transcribe-vocabulary-filter-method: VocabularyFilterMethod
x-amzn-transcribe-language-model-name: LanguageModelName
x-amzn-transcribe-enable-channel-identification: EnableChannelIdentification
x-amzn-transcribe-number-of-channels: NumberOfChannels
x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
x-amzn-transcribe-enable-partial-results-stabilization: EnablePartialResultsStabilization
x-amzn-transcribe-partial-results-stability: PartialResultsStability
x-amzn-transcribe-content-identification-type: ContentIdentificationType (or x-amzn-transcribe-content-redaction-type: ContentRedactionType)
x-amzn-transcribe-pii-entity-types: PiiEntityTypes
Content-type: application/json
```

To start an HTTP/2 stream with PII identification or PII redaction activated, use the [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) operation and specify the following:
+ For `LanguageCode`, specify the language code for the language spoken in the stream\. For US English, specify `en-US`\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ For `ContentIdentificationType`, specify `PII`\. Specify this field if you're identifying PII in the transcription results\. You can only use this parameter if you **are not** using `content-redaction-type`\.
+ For `ContentRedactionType`, specify `PII`\. Specify this field if you're redacting PII in the transcription results\. You can only use this parameter if you **are not** using `content-identification-type`\.
+ For `PiiEntityTypes`, specify the types of PII you want to identify\. You can specify one or more values\. `pii-entity-types` is an optional parameter with a default of `ALL`; if you don't specify which entities you want to redact \(or identify\), all PII entity types are redacted \(or identified\)\.

  The available values for `PiiEntityTypes` are: `BANK_ACCOUNT_NUMBER`, `BANK_ROUTING`, `CREDIT_DEBIT_NUMBER`, `CREDIT_DEBIT_CVV`, `CREDIT_DEBIT_EXPIRY`, `PIN`, `EMAIL`, `ADDRESS`, `NAME`, `PHONE`, `SSN`, and `ALL`\. `PiiEntityTypes` is an optional parameter with a default value of `ALL`\.

**Note**  
PII redaction for streaming is only supported in these AWS Regions: Asia Pacific \(Seoul\), Asia Pacific \(Sydney\), Asia Pacific \(Tokyo\), Canada \(Central\), EU \(Frankfurt\), EU \(Ireland\), EU \(London\), US East \(N\. Virginia\), US East \(Ohio\), and US West \(Oregon\)\.