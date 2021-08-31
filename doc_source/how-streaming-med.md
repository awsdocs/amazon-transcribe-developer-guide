# Using Amazon Transcribe Medical streaming with HTTP/2<a name="how-streaming-med"></a>

 Amazon Transcribe Medical uses a format called *event stream encoding* for streaming\-med transcription\. This format encoded binary data with header information that describes the contents of each event\. For more information, see [Event stream encoding](event-stream.md)\. You can use this information for applications that call the Amazon Transcribe Medical endpoint without using the Amazon Transcribe Medical SDK\. 

When Amazon Transcribe Medical uses the [HTTP/2 protocol](https://http2.github.io/) for streaming medical transcriptions, the key components for a streaming medical request are:
+ A header frame\. This contains the HTTP/2 headers for the request, and a signature in the `authorization` header that Amazon Transcribe Medical uses as a seed signature to sign the following data frames\.
+ One or more message frames in event stream encoding\. The frame contains metadata and the raw audio bytes\.
+ An end frame\. This is a signed message in event stream encoding with an empty body\.

## Streaming request<a name="streaming-med-request"></a>

To make a streaming request, you use the [ StartMedicalStreamTranscription ](API_streaming_StartMedicalStreamTranscription.md) API\. 

### Header frame<a name="streaming-med-header"></a>

The header frame is the authorization frame for the streaming transcription\. Amazon Transcribe Medical uses the value of the `authorization` header as the seed for generating a chain of authorization headers for the data frames in the request\. 

#### Required headers<a name="required-headers"></a>

The header frame of a request to Amazon Transcribe Medical requires the following HTTP/2 headers\.

```
POST /stream-transcription HTTP/2.0
host: transcribestreaming.region.amazonaws.com
authorization: Generated value
content-type: application/vnd.amazon.eventstream
x-amz-target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
x-amz-content-sha256: streaming-med-AWS4-HMAC-SHA256-EVENTS
x-amz-date: Date
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: media encoding
x-amzn-transcribe-sample-rate: Sample rate
transfer-encoding: chunked
```

In the request, use the following values for the `host`, `authorization`, and `x-amz-date` headers:
+ **`host`**: Use the AWS Region where you are calling Amazon Transcribe Medical\. For a list of valid regions, see [ AWS Regions and Endpoints ](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region) in the *Amazon Web Services General Reference*\. 
+ **`authorization`**: The Signature Version 4 signature for the request\. For more information about creating a signature, see [ Signing AWS Requests with Signature Version 4 ](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html) in the *Amazon Web Services General Reference*\.
+ **`x-amz-date`**: Generate a date and time for the request following the instructions in [Handling Dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html) in the *Amazon Web Services General Reference*\.

For more information about the headers specific to Amazon Transcribe Medical, see the [ StartMedicalStreamTranscription ](API_streaming_StartMedicalStreamTranscription.md) API\.

### Data frames<a name="streaming-med-data"></a>

Each request contains one or more data frames\. The data frames use event stream encoding\. The encoding supports bidirectional data transmission between a client and a server\. 

There are two steps to creating a data frame:

1. Combine the raw audio data with metadata to create the payload of the request\. 

1. Combine the payload with a signature to form the event message that is sent to Amazon Transcribe Medical\.

The following diagram shows how this works\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/streaming10.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

#### Create the audio event<a name="audio-event"></a>

To create the message to send to Amazon Transcribe Medical, create the audio event\. Combine the headers described in the following table with a chunk of audio bytes into an event\-encoded message\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-diagram-event-headers.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

To create the payload for the event message, use a buffer in raw\-byte format\.

#### Create the message<a name="dataframe"></a>

Create a data frame using the audio event payload to send to Amazon Transcribe Medical\. The data frame contains event\-encoding headers that include the current date and a signature for the audio chunk and the audio event\. To indicate to Amazon Transcribe Medical that the audio stream is complete, send an empty data frame that contains only the date and signature\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-diagram-message-headers.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

To create the signature for the data frame, first create a string to sign, and then calculate the signature for the event\. Construct the string to sign as follows\.

```
String stringToSign =
    "AWS4-HMAC-SHA256-PAYLOAD" +
    "\n" +
    DATE +
    "\n" +
    KEYPATH +
    "\n" +
    Hex(priorSignature) +
    "\n" +
    HexHash(nonSignatureHeaders) +
    "\n" +
    HexHash(payload);
```
+ **`DATE`**: The current date and time in Universal Time Coordinated \(UTC\) and using the [ISO 8601 format](https://www.iso.org/iso-8601-date-and-time-format.html)\. Don't include milliseconds in the date\. For example, 20190127T223754Z is 22:37:54 on 1/27/2019\.
+ **`KEYPATH`**: The signature scope in the format `date/region/service/aws4_request`\. For example, `20190127/us-east-1/transcribe/aws4_request`\.
+ **`priorSignature`**: The signature for the previous frame\. For the first data frame, use the signature of the header frame\.
+ **`nonSignatureHeaders`**: The `DATE` header encoded as a string\.
+ **`payload`**: The byte buffer containing the audio event data\.
+ **`Hex`**: A function that encodes its input into a hexadecimal representation\.
+ **`HexHash`**: A function that first creates a SHA\-256 hash of its input and then uses the `Hex` function to encode the hash\.

After you have constructed the string to sign, sign it using the key that you derived for Signature Version 4, as follows\. For details, see [Examples of How to Derive a Signing Key for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/signature-v4-examples.html) in the *Amazon Web Services General Reference*\.

```
String signature = HMACSHA256(derivedSigningKey, stringToSign);
```
+ **`HMACSHA256`**: A function that creates a signature using the SHA\-256 hash function\.
+ **`derivedSigningKey`**: The Signature Version 4 signing key\.
+ **`stringToSign`**: The string that you calculated for the data frame\.

After you have calculated the signature for the data frame, construct a byte buffer containing the date, the signature, and the audio event payload\. Send the byte array to Amazon Transcribe Medical for transcription\.

### End frame<a name="end-frame"></a>

To indicate that the audio stream is complete, send an end frame to Amazon Transcribe Medical\. The *end frame* is a data frame with an empty payload\. You construct the end frame the same way that you construct a data frame\.

## Streaming response<a name="streaming-med-response"></a>

Responses from Amazon Transcribe Medical are also sent using event stream encoding\. Use this information to decode a response from the [ StartMedicalStreamTranscription ](API_streaming_StartMedicalStreamTranscription.md) API\.

### Transcription response<a name="transcription-response"></a>

A transcription response is event stream encoded\. It contains the standard prelude and the following headers\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-response-headers.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

For details, see [Event stream encoding](event-stream.md)\. 

When the response is decoded, it contains the following information:

```
:content-type: "application/json"
:event-type: "TranscriptEvent"
:message-type: "event"
                
JSON transcription information
```

For an example of the JSON structure returned by Amazon Transcribe Medical, see [Using Amazon Transcribe Medical streaming with HTTP/2](#how-streaming-med)\. 

### Exception response<a name="streaming-med-exception"></a>

If there is an error in processing your transcription stream, Amazon Transcribe Medical sends an exception response\. The response is event stream encoded\. For details, see [Event stream encoding](event-stream.md)\. 

The response contains the standard prelude and the following headers\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-error-headers.png)

When the exception response is decoded, it contains the following information\.

```
:content-type: "application/json"
:event-type: "BadRequestException"
:message-type: "exception"
                
Exception message
```

## Example request and response<a name="streaming-med-example"></a>

The following is an end\-to\-end example of a streaming transcription request\. In this example, binary data is represented as base64\-encoded strings\. In an actual response, the data are raw bytes\.

### Step 1: Start the session with Amazon Transcribe Medical<a name="streaming-med-example-step1"></a>

To start the session, send an HTTP/2 request to Amazon Transcribe Medical\.

```
POST /stream-transcription HTTP/2.0
host: transcribestreaming.region.amazonaws.com
authorization: Generated value
content-type: application/vnd.amazon.eventstream
x-amz-content-sha256: streaming-med-AWS4-HMAC-SHA256-EVENTS
x-amz-date: Date
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: Media encoding
x-amzn-transcribe-sample-rate: Sample rate
transfer-encoding: chunked
```

### Step 2: Send authentication information to Amazon Transcribe Medical<a name="streaming-med-example-step2"></a>

Amazon Transcribe Medical sends the following response\.

```
HTTP/2.0 200
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-sample-rate: Sample rate
x-amzn-request-id: 8a08df7d-5998-48bf-a303-484355b4ab4e
x-amzn-transcribe-session-id: b4526fcf-5eee-4361-8192-d1cb9e9d6887
x-amzn-transcribe-media-encoding: pcm
x-amzn-RequestId: 8a08df7d-5998-48bf-a303-484355b4ab4e
content-type: application/vnd.amazon.eventstream
```

### Step 3: Create an audio event<a name="streaming-med-example-step3"></a>

Create an audio event containing the audio data to send\. For details, see [Event stream encoding](event-stream-med.md)\. The binary data in this request is base64\-encoded\. In an actual request, the data is raw bytes\.

```
:content-type: "application/octet-stream"
:event-type: "AudioEvent"
:message-type: "event"

UklGRjzxPQBXQVZFZm10IBAAAAABAAEAgD4AAAB9AAACABAAZGF0YVTwPQAAAAAAAAAAAAAAAAD//wIA/f8EAA==
```

### Step 4: Create an audio event message<a name="streaming-med-example-step4"></a>

Create an audio message that contains the audio data to send to Amazon Transcribe Medical\. For details, see [Event stream encoding](event-stream-med.md)\. The audio event data in this example is base64\-encoded\. In an actual request, the data is raw bytes\.

```
:date: 2019-01-29T01:56:17.291Z
:chunk-signature: signature

AAAA0gAAAIKVoRFcTTcjb250ZW50LXR5cGUHABhhcHBsaWNhdGlvbi9vY3RldC1zdHJlYW0LOmV2ZW50LXR5
cGUHAApBdWRpb0V2ZW50DTptZXNzYWdlLXR5cGUHAAVldmVudAxDb256ZW50LVR5cGUHABphcHBsaWNhdGlv
bi94LWFtei1qc29uLTEuMVJJRkY88T0AV0FWRWZtdCAQAAAAAQABAIA+AAAAfQAAAgAQAGRhdGFU8D0AAAAA
AAAAAAAAAAAA//8CAP3/BAC7QLFf
```

### Step 5: Use the response from Amazon Transcribe Medical<a name="streaming-med-example-step5"></a>

Amazon Transcribe Medical creates a stream of transcription events that it sends to your application\. The events are sent in raw\-byte format\. In this example, the bytes are base64\-encoded\.

Amazon Transcribe Medical sends the following response\.

```
AAAAUwAAAEP1RHpYBTpkYXRlCAAAAWiXUkMLEDpjaHVuay1zaWduYXR1cmUGACCt6Zy+uymwEK2SrLp/zVBI
5eGn83jdBwCaRUBJA+eaDafqjqI=
```

To see the transcription results, decode the raw bytes using event\-stream encoding\. 

```
:event-type: "TranscriptEvent"
:content-type: "application/json"
:message-type: "event"

{"Transcript":{"Results":[results]}}
```

For an example of the JSON structure returned by Amazon Transcribe Medical, see [Event stream encoding](event-stream-med.md)\. 

### Step 6: End the transcription stream<a name="streaming-med-example-step6"></a>

Finally, send an empty audio event to Amazon Transcribe Medical to end the transcription stream\. Create the audio event exactly like any other, except with an empty payload\. Sign the event and include the signature in the `:chunk-signature` header, as follows\.

```
:date: 2019-01-29T01:56:17.291Z
:chunk-signature: signature
```