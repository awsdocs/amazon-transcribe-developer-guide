# Setting up a streaming transcription<a name="streaming-setting-up"></a>

This section expands on the main [streaming](streaming.md) section\. It's intended to provide information for users who want to set up their stream with HTTP/2 or WebSockets directly, rather than with an AWS SDK\. The information in this section can also be used to build your own SDK\.

Note that we strongly recommend using SDKs rather than using HTTP/2 and WebSockets directly\. SDKs are the simplest and most reliable method for transcribing data streams\. To start streaming using an AWS SDK, see [Transcribing with the AWS SDKs](getting-started-sdk.md)\. 

## Event stream encoding<a name="streaming-event-stream"></a>

Amazon Transcribe uses a format called event stream encoding for streaming transcriptions\.

Event stream encoding provides bidirectional communication between a client and a server\. Data frames sent to the Amazon Transcribe streaming service are encoded in this format\. The response from Amazon Transcribe also uses this encoding\.

Each message consists of two sections: the prelude and the data\. The prelude consists of:

1. The total byte length of the message

1. The combined byte length of all headers

The data section consists of:

1. Headers

1. Payload

Each section ends with a 4\-byte big\-endian integer cyclic redundancy check \(CRC\) checksum\. The message CRC checksum is for both the prelude section and the data section\. Amazon Transcribe uses CRC32 \(often referred to as GZIP CRC32\) to calculate both CRCs\. For more information about CRC32, see [https://www.ietf.org/rfc/rfc1952.txt](https://www.ietf.org/rfc/rfc1952.txt)\.

Total message overhead, including the prelude and both checksums, is 16 bytes\.

The following diagram shows the components that make up a message and a header\. There are multiple headers per message\.

![\[A schematic of the components of a message and a header for a streaming transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/frame-diagram-frame-overview.png)![\[A schematic of the components of a message and a header for a streaming transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

Each message contains the following components:
+ **Prelude**: Consists of two, 4\-byte fields, for a fixed total of 8 bytes\.
  + *First 4 bytes*: The big\-endian integer byte\-length of the entire message, inclusive of this 4\-byte length field\.
  + *Second 4 bytes*: The big\-endian integer byte\-length of the 'headers' portion of the message, excluding the 'headers' length field itself\.
+ **Prelude CRC**: The 4\-byte CRC checksum for the prelude portion of the message, excluding the CRC itself\. The prelude has a separate CRC from the message CRC\. That ensures that Amazon Transcribe can detect corrupted byte\-length information immediately without causing errors, such as buffer overruns\.
+ **Headers**: Metadata annotating the message; for example, message type and content type\. Messages have multiple headers, which are key:value pairs, where the key is a UTF\-8 string\. Headers can appear in any order in the 'headers' portion of the message, and each header can appear only once\.
+ **Payload**: The audio content to be transcribed\.
+ **Message CRC**: The 4\-byte CRC checksum from the start of the message to the start of the checksum\. That is, everything in the message except the CRC itself\.

The header frame is the authorization frame for the streaming transcription\. Amazon Transcribe uses the authorization header's value as the seed for generating a chain of authorization headers for the data frames in the request\.

Each header contains the following components; there are multiple headers per frame\.
+ **Header name byte\-length**: The byte\-length of the header name\.
+ **Header name**: The name of the header that indicates the header type\. For valid values, see the following frame descriptions\.
+ **Header value type**: A number indicating the header value\. The following list shows the possible values for the header and what they indicate\.
  + `0` – TRUE
  + `1` – FALSE
  + `2` – BYTE
  + `3` – SHORT
  + `4` – INTEGER
  + `5` – LONG
  + `6` – BYTE ARRAY
  + `7` – STRING
  + `8` – TIMESTAMP
  + `9` – UUID
+ **Value string byte length**: The byte length of the header value string\.
+ **Header value**: The value of the header string\. Valid values for this field depend on the type of header\. See [Setting up an HTTP/2 stream](streaming-http2.md) or [Setting up a WebSocket stream](streaming-websocket.md) for more information\.

## Data frames<a name="streaming-data-frames"></a>

Each streaming request contains one or more data frames\. There are two steps to creating a data frame:

1. Combine raw audio data with metadata to create the payload of your request\.

1. Combine the payload with a signature to form the event message that is sent to Amazon Transcribe\.

The following diagram shows how this works\.

![\[The components of a data frame for a streaming transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/streaming10.png)![\[The components of a data frame for a streaming transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

You can find more information on data frames in the [Setting up an HTTP/2 stream](streaming-http2.md) and [Setting up a WebSocket stream](streaming-websocket.md) sections\.