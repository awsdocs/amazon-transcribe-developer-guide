# Using Amazon Transcribe Streaming With HTTP/2<a name="how-streaming"></a>

 Amazon Transcribe uses a format called *event stream encoding* for streaming transcription\. This format encoded binary data with header information that describes the contents of each event\. For more information, see [Event Stream Encoding](event-stream.md)\. You can use this information for applications that call the Amazon Transcribe endpoint without using the Amazon Transcribe SDK\. 

When Amazon Transcribe uses the [HTTP/2 protocol](https://http2.github.io/http2-spec/) for streaming transcriptions, the key components for a streaming request are:
+ A header frame\. This contains the HTTP/2 headers for the request, and a signature in the `authorization` header that Amazon Transcribe uses as a seed signature to sign the following data frames\.
+ One or more message frames in event stream encoding\. The frame contains metadata and the raw audio bytes\.
+ An end frame\. This is a signed message in event stream encoding with an empty body\.

## Streaming Request<a name="streaming-request"></a>

To make a streaming request, you use the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation\. 

### Header Frame<a name="streaming-header"></a>

The header frame is the authorization frame for the streaming transcription\. Amazon Transcribe uses the value of the `authorization` header as the seed for generating a chain of authorization headers for the data frames in the request\. 

#### Required Headers<a name="required-headers"></a>

The header frame of a request to Amazon Transcribe requires the following HTTP/2 headers:

```
POST /stream-transcription HTTP/2.0
host: transcribestreaming.region.amazonaws.com
authorization: Generated value
content-type: application/vnd.amazon.eventstream
x-amz-target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
x-amz-content-sha256: STREAMING-AWS4-HMAC-SHA256-EVENTS
x-amz-date: Date
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: pcm
x-amzn-transcribe-sample-rate: Sample rate
transfer-encoding: chunked
```

In the request, use the following values for the `host`, `authorization`, and `x-amz-date` headers:
+ **`host`**: Use the AWS Region where you are calling Amazon Transcribe\. For a list of valid regions, see [ AWS Regions and Endpoints ](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region) in the *Amazon Web Services General Reference*\. 
+ **`authorization`**: The Signature Version 4 signature for the request\. For more information about creating a signature, see [ Signing AWS Requests with Signature Version 4 ](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html) in the *Amazon Web Services General Reference*\.
+ **`x-amz-date`**: Generate a date and time for the request following the instructions in [Handling Dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html) in the *Amazon Web Services General Reference*\.

For more information about the headers specific to Amazon Transcribe, see the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation\.

### Data Frames<a name="streaming-data"></a>

Each request contains one or more data frames\. The data frames use event stream encoding\. The encoding supports bidirectional data transmission between a client and a server\. 

There are two steps to creating a data frame:

1. Combine the raw audio data with metadata to create the payload of the request\. 

1. Combine the payload with a signature to form the event message that is sent to Amazon Transcribe\.

The following diagram shows how this works\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/streaming10.png)

#### Create the Audio Event<a name="audio-event"></a>

To create the message to send to Amazon Transcribe, create the audio event\. Combine the headers described in the following table with a chunk of audio bytes into an event\-encoded message\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-diagram-event-headers.png)

To create the payload for the event message, use a buffer in raw\-byte format\.

#### Create the Message<a name="dataframe"></a>

Create a data frame using the audio event payload to send to Amazon Transcribe\. The data frame contains event\-encoding headers that include the current date and a signature for the audio chunk and the audio event\. To indicate to Amazon Transcribe that the audio stream is complete, send an empty data frame that contains only the date and signature\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-diagram-message-headers.png)

To create the signature for the data frame, first create a string to sign, and then calculate the signature for the event\. Construct the string to sign as follows:

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

After you have calculated the signature for the data frame, construct a byte buffer containing the date, the signature, and the audio event payload\. Send the byte array to Amazon Transcribe for transcription\.

### End Frame<a name="end-frame"></a>

To indicate that the audio stream is complete, send an end frame to Amazon Transcribe\. The *end frame* is a data frame with an empty payload\. You construct the end frame the same way that you construct a data frame\.

## Streaming Response<a name="streaming-response"></a>

Responses from Amazon Transcribe are also sent using event stream encoding\. Use this information to decode a response from the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation\.

### Transcription Response<a name="transcription-response"></a>

A transcription response is event stream encoded\. It contains the standard prelude and the following headers:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-response-headers.png)

For details, see [Event Stream Encoding](event-stream.md)\. 

When the response is decoded, it contains the following information:

```
:content-type: "application/json"
:event-type: "TranscriptEvent"
:message-type: "event"
                
JSON transcription information
```

For an example of the JSON structure returned by Amazon Transcribe, see [Using Amazon Transcribe Streaming With HTTP/2](#how-streaming)\. 

### Exception Response<a name="streaming-exception"></a>

If there is an error in processing your transcription stream, Amazon Transcribe sends an exception response\. The response is event stream encoded\. For details, see [Event Stream Encoding](event-stream.md)\. 

The response contains the standard prelude and the following headers:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-error-headers.png)

When the exception response is decoded, it contains the following information:

```
:content-type: "application/json"
:event-type: "BadRequestException"
:message-type: "exception"
                
Exception message
```

## Example Request and Response<a name="streaming-example"></a>

The following is an end\-to\-end example of a streaming transcription request\. In this example, binary data is represented as base64\-encoded strings\. In an actual response, the data are raw bytes\.

### Step 1 \- Start the Session With Amazon Transcribe<a name="streaming-example-step1"></a>

To start the session, send an HTTP/2 request to Amazon Transcribe: 

```
POST /stream-transcription HTTP/2.0
host: transcribestreaming.region.amazonaws.com
authorization: Generated value
content-type: application/vnd.amazon.eventstream
x-amz-content-sha256: STREAMING-AWS4-HMAC-SHA256-EVENTS
x-amz-date: Date
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: pcm
x-amzn-transcribe-sample-rate: Sample rate
transfer-encoding: chunked
```

### Step 2 \- Send Authentication Information to Amazon Transcribe<a name="streaming-example-step2"></a>

Amazon Transcribe sends the following response:

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

### Step 3 \- Create an Audio Event<a name="streaming-example-step3"></a>

Create an audio event containing the audio data to send\. For details, see [Event Stream Encoding](event-stream.md)\. The binary data in this request is base64\-encoded\. In an actual request, the data is raw bytes\.

```
:content-type: "application/octet-stream"
:event-type: "AudioEvent"
:message-type: "event"

UklGRjzxPQBXQVZFZm10IBAAAAABAAEAgD4AAAB9AAACABAAZGF0YVTwPQAAAAAAAAAAAAAAAAD//wIA/f8EAA==
```

### Step 4 \- Create an Audio Event Message<a name="streaming-example-step4"></a>

Create an audio message that contains the audio data to send to Amazon Transcribe\. For details, see [Event Stream Encoding](event-stream.md)\. The audio event data in this example is base64\-encoded\. In an actual request, the data is raw bytes\.

```
:date: 2019-01-29T01:56:17.291Z
:chunk-signature: signature

AAAA0gAAAIKVoRFcTTcjb250ZW50LXR5cGUHABhhcHBsaWNhdGlvbi9vY3RldC1zdHJlYW0LOmV2ZW50LXR5
cGUHAApBdWRpb0V2ZW50DTptZXNzYWdlLXR5cGUHAAVldmVudAxDb256ZW50LVR5cGUHABphcHBsaWNhdGlv
bi94LWFtei1qc29uLTEuMVJJRkY88T0AV0FWRWZtdCAQAAAAAQABAIA+AAAAfQAAAgAQAGRhdGFU8D0AAAAA
AAAAAAAAAAAA//8CAP3/BAC7QLFf
```

### Step 5 \- Use the Response from Amazon Transcribe<a name="streaming-example-step5"></a>

Amazon Transcribe creates a stream of transcription events that it sends to your application\. The events are sent in raw\-byte format\. In this example, the bytes are base64\-encoded\.

The response from Amazon Transcribe is:

```
AAAAUwAAAEP1RHpYBTpkYXRlCAAAAWiXUkMLEDpjaHVuay1zaWduYXR1cmUGACCt6Zy+uymwEK2SrLp/zVBI
5eGn83jdBwCaRUBJA+eaDafqjqI=
```

To see the transcription results, decode the raw bytes using event\-stream encoding: 

```
:event-type: "TranscriptEvent"
:content-type: "application/json"
:message-type: "event"

{"Transcript":{"Results":[results]}}
```

For an example of the JSON structure returned by Amazon Transcribe, see [Event Stream Encoding](event-stream.md)\. 

### Step 6 \- End the Transcription Stream<a name="streaming-example-step6"></a>

Finally, send an empty audio event to Amazon Transcribe to end the transcription stream\. Create the audio event exactly like any other, except with an empty payload\. Sign the event and include the signature in the `:chunk-signature` header, as follows:

```
:date: 2019-01-29T01:56:17.291Z
:chunk-signature: signature
```