# Setting up an HTTP/2 stream<a name="streaming-http2"></a>

The key components for an [HTTP/2 protocol](https://http2.github.io/) for streaming transcription requests with Amazon Transcribe are:
+ A header frame\. This contains the HTTP/2 headers for your request, and a signature in the authorization header that Amazon Transcribe uses as a seed signature to sign the data frames\.
+ One or more message frames in [event stream encoding](streaming-setting-up.md#streaming-event-stream) that contain metadata and raw audio bytes\.
+ An end frame\. This is a signed message in [event stream encoding](streaming-setting-up.md#streaming-event-stream) with an empty body\.

**Note**  
Amazon Transcribe only supports one stream per HTTP/2 session\. If you attempt to use multiple streams, your transcription request fails\.

1. Attach the following policy to the IAM role that makes the request\. See [ Adding IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html#add-policy-api) for more information\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "my-transcribe-http2-policy",
               "Effect": "Allow",
               "Action": "transcribe:StartStreamTranscription",
               "Resource": "*"
           }
       ]
   }
   ```

1. To start the session, send an HTTP/2 request to Amazon Transcribe\.

   ```
   POST /stream-transcription HTTP/2
   host: transcribestreaming.us-west-2.amazonaws.com
   X-Amz-Target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
   Content-Type: application/vnd.amazon.eventstream
   X-Amz-Content-Sha256: string
   X-Amz-Date: YYYYMMDDTHHMMSSZ
   Authorization: AWS4-HMAC-SHA256 Credential=access-key/YYYYMMDD/us-west-2/transcribe/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date;x-amz-target;x-amz-security-token, Signature=string
   x-amzn-transcribe-language-code: en-US
   x-amzn-transcribe-media-encoding: flac
   x-amzn-transcribe-sample-rate: 16000
   transfer-encoding: chunked
   ```

   Additional operations and parameters are listed in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

   Amazon Transcribe sends the following response:

   ```
   HTTP/2.0 200
   x-amzn-transcribe-language-code: en-US
   x-amzn-transcribe-media-encoding: flac
   x-amzn-transcribe-sample-rate: 16000
   x-amzn-request-id: 8a08df7d-5998-48bf-a303-484355b4ab4e
   x-amzn-transcribe-session-id: b4526fcf-5eee-4361-8192-d1cb9e9d6887
   content-type: application/json
   ```

1. Create an audio event that contains your audio data\. Combine the headers—described in the following table—with a chunk of audio bytes in an event\-encoded message\. To create the payload for the event message, use a buffer in raw\-byte format\.    
<a name="table-http2-frame-diagram-event-headers"></a>[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/streaming-http2.html)

   Binary data in this example request are base64\-encoded\. In an actual request, data are raw bytes\.

   ```
   :content-type: "application/vnd.amazon.eventstream"
   :event-type: "AudioEvent"
   :message-type: "event"
   UklGRjzxPQBXQVZFZm10IBAAAAABAAEAgD4AAAB9AAACABAAZGF0YVTwPQAAAAAAAAAAAAAAAAD//wIA/f8EAA==
   ```

1. Create an audio message that contains your audio data\.

   1. Your audio message data frame contains event\-encoding headers that include the current date and a signature for the audio chunk and the audio event\.    
<a name="table-http2-diagram-message-headers"></a>[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/streaming-http2.html)

      Binary data in this request are base64\-encoded\. In an actual request, data are raw bytes\.

      ```
      :date: 2019-01-29T01:56:17.291Z
      :chunk-signature: signature
      
      AAAA0gAAAIKVoRFcTTcjb250ZW50LXR5cGUHABhhcHBsaWNhdGlvbi9vY3RldC1zdHJlYW0LOmV2ZW50LXR5
      cGUHAApBdWRpb0V2ZW50DTptZXNzYWdlLXR5cGUHAAVldmVudAxDb256ZW50LVR5cGUHABphcHBsaWNhdGlv
      bi94LWFtei1qc29uLTEuMVJJRkY88T0AV0FWRWZtdCAQAAAAAQABAIA+AAAAfQAAAgAQAGRhdGFU8D0AAAAA
      AAAAAAAAAAAA//8CAP3/BAC7QLFf
      ```

   1. Construct a string to sign, as outlined in [Create a string to sign for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-create-string-to-sign.html)\. Your string follows this format:

      ```
      String stringToSign =
      "AWS4-HMAC-SHA256" +
      "\n" +
      DateTime +
      "\n" +
      Keypath +
      "\n" +
      Hex(priorSignature) +
      "\n" +
      HexHash(nonSignatureHeaders) +
      "\n" +
      HexHash(payload);
      ```
      + **DateTime**: The date and time the signature is created\. The format is YYYYMMDDTHHMMSSZ, where YYYY=year, MM=month, DD=day, HH=hour, MM=minute, SS=seconds, and 'T' and 'Z' are fixed characters\. For more information, refer to [Handling Dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html)\.
      + **Keypath**: The signature scope in the format `date/region/service/aws4_request`\. For example, `20220127/us-west-2/transcribe/aws4_request`\.
      + **Hex**: A function that encodes input into a hexadecimal representation\.
      + **priorSignature**: The signature for the previous frame\. For the first data frame, use the signature of the header frame\.
      + **HexHash**: A function that first creates a SHA\-256 hash of its input and then uses the Hex function to encode the hash\.
      + **nonSignatureHeaders**: The DateTime header encoded as a string\.
      + **payload**: The byte buffer containing the audio event data\.

   1. Derive a signing key from your AWS secret access key and use it to sign the `stringToSign`\. For a greater degree of protection, the derived key is specific to the date, service, and AWS Region\. For more information, see [Calculate the signature for AWSSignature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-calculate-signature.html)\.

      Make sure you implement the `GetSignatureKey` function to derive your signing key\. If you have not yet derived a signing key, refer to [Examples of how to derive a signing key for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/signature-v4-examples.html)\.

      ```
      String signature = HMACSHA256(derivedSigningKey, stringToSign);
      ```
      + **HMACSHA256**: A function that creates a signature using the SHA\-256 hash function\.
      + **derivedSigningKey**: The Signature Version 4 signing key\.
      + **stringToSign**: The string you calculated for the data frame\.

      After you've calculated the signature for the data frame, construct a byte buffer containing the date, signature, and audio event payload\. Send the byte array to Amazon Transcribe for transcription\.

1. To indicate the audio stream is complete, send an end frame \(an empty data frame\) that contains only the date and signature\. You construct this end frame the same way you construct a data frame\.

   Amazon Transcribe responds with a stream of transcription events, sent to your application\. This response is event stream encoded\. It contains the standard prelude and the following headers\.    
<a name="table-http2-frame-response-headers"></a>[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/streaming-http2.html)

   The events are sent in raw\-byte format\. In this example, the bytes are base64\-encoded\.

   ```
   AAAAUwAAAEP1RHpYBTpkYXRlCAAAAWiXUkMLEDpjaHVuay1zaWduYXR1cmUGACCt6Zy+uymwEK2SrLp/zVBI
   5eGn83jdBwCaRUBJA+eaDafqjqI=
   ```

   To see the transcription results, decode the raw bytes using event stream encoding\.

   ```
   :content-type: "application/vnd.amazon.eventstream"
   :event-type: "TranscriptEvent"
   :message-type: "event"
   
   {
       "Transcript":
           {
               "Results":
                   [
                       results
                   ]
           }
   }
   ```

1. To end your stream, send an empty audio event to Amazon Transcribe\. Create the audio event exactly like any other, except with an empty payload\. Sign the event and include the signature in the `:chunk-signature` header, as follows:

   ```
   :date: 2019-01-29T01:56:17.291Z
   :chunk-signature: signature
   ```

## Handling HTTP/2 streaming errors<a name="http2-errors"></a>

If an error occurs when processing your media stream, Amazon Transcribe sends an exception response\. The response is event stream encoded\.

The response contains the standard prelude and the following headers:


| Header name byte length | Header name \(string\) | Header value type | Value string byte length | Value string \(UTF\-8\) | 
| --- | --- | --- | --- | --- | 
| 13 | :content\-type | 7 | 16 | application/json | 
| 11 | :event\-type | 7 | 19 | BadRequestException | 
| 13 | :message\-type | 7 | 9 | exception | 

When the exception response is decoded, it contains the following information:

```
:content-type: "application/vnd.amazon.eventstream"
:event-type: "BadRequestException"
:message-type: "exception"
                
Exception message
```