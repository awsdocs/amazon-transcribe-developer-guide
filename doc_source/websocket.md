# Using Amazon Transcribe streaming with WebSockets<a name="websocket"></a>

When you use the [WebSocket protocol](https://tools.ietf.org/html/rfc6455) to stream audio, Amazon Transcribe transcribes the stream in real time\. You encode the audio with event stream encoding, Amazon Transcribe responds with a JSON structure that is also encoded using event stream encoding\. For more information, see [Event stream encoding](event-stream.md)\. You can use the information in this section to create applications using the WebSocket library of your choice\.



**Topics**
+ [Adding a policy for WebSocket requests to your IAM role](#websocket-iam)
+ [Creating a pre\-signed URL](#websocket-url)
+ [Handling the WebSocket upgrade response](#websocket-response)
+ [Making a WebSocket streaming request](#websocket-streaming-request)
+ [Handling a WebSocket streaming response](#websocket-streaming-response)
+ [Handling WebSocket streaming errors](#websocket-errors)

## Adding a policy for WebSocket requests to your IAM role<a name="websocket-iam"></a>

To use the WebSocket protocol to call Amazon Transcribe, you need to attach the following policy to the AWS Identity and Access Management \(IAM\) role that makes the request\. See [ Adding IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html#add-policy-api) for more information on how to do this\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "transcribestreaming",
            "Effect": "Allow",
            "Action": "transcribe:StartStreamTranscriptionWebSocket",
            "Resource": "*"
        }
    ]
}
```

## Creating a pre\-signed URL<a name="websocket-url"></a>

Construct a URL for your WebSocket request that contains the information needed to set up communication between your application and Amazon Transcribe\. WebSocket streaming uses the Amazon Signature Version 4 process for signing requests\. Signing the request helps to verify the identity of the requester and to protect your audio data in transit\. It also protects against potential replay attacks\. For more information about Signature Version 4, see [ Signing AWS API Requests](https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html) in the *Amazon Web Services General Reference*\.

The URL has the following format\. Line breaks have been added for readability\.

```
GET wss://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket
?language-code=languageCode
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
   &vocabulary-name=vocabularyName
```

Use the following values for the URL parameters:
+ **language\-code** – The language code for the input audio\. Valid values are `en-AU, en-GB, en-US, es-US, fr-CA, fr-FR, de-DE, ja-JP, ko-KR, pt-BR, zh-CN` and `it-IT`\.
+ **media\-encoding** – The encoding used for the input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **sample\-rate** – The sample rate of the input audio in Hertz\. We suggest that you use 8000 Hz for low\-quality audio and 16000 Hz for high\-quality audio\. The sample rate must match the sample rate in the audio file\.
+ **sessionId** – Optional\. An identifier for the transcription session\. If you don't provide a session ID, Amazon Transcribe generates one for you and returns it in the response\.
+ **vocabulary\-name** – Optional\. The name of the vocabulary to use when processing the transcription job, if any\.

 The remaining parameters are Signature Version 4 parameters: 
+ **X\-Amz\-Algorithm** – The algorithm you're using in the signing process\. The only valid value is `AWS4-HMAC-SHA256`\.
+ **X\-Amz\-Credential** – A string separated by slashes \("/"\) that is formed by concatenating your access key ID and your credential scope components\. Credential scope includes the date in YYYYMMDD format, the AWS Region, the service name, and a special termination string \(aws4\_request\)\.
+ **X\-Amz\-Date** – The date and time that the signature was created\. Generate the date and time by following the instructions in [Handling Dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html) in the *Amazon Web Services General Reference*\.
+ **X\-Amz\-Expires** – The length of time in seconds until the credentials expire\. The maximum value is 300 seconds \(5 minutes\)\.
+ **X\-Amz\-Security\-Token** – Optional\. A Signature Version 4 token for temporary credentials\. If you specify this parameter, include it in the canonical request\. For more information, see [Requesting Temporary Security Credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_request.html) in the *AWS Identity and Access Management User Guide*\.
+ **X\-Amz\-Signature** – The Signature Version 4 signature that you generated for the request\.
+ **X\-Amz\-SignedHeaders** – The headers that are signed when creating the signature for the request\. The only valid value is `host`\.

To construct the URL for the request and create the Signature Version 4 signature, use the following steps\. The examples are in pseudocode\. 

**Task 1: Create a canonical request**

Create a string that includes information from your request in a standardized format\. This ensures that when AWS receives the request, it can calculate the same signature that you calculate in Task 3\. For more information, see [Create a Canonical Request for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-create-canonical-request.html) in the *Amazon Web Services General Reference*\.

1. Define variables for the request in your application\.

   ```
   # HTTP verb
   method = "GET"
   # Service name
   service = "transcribe"
   # AWS Region
   region = "AWS Region"
   # Amazon Transcribe streaming endpoint
   endpoint = "wss://transcribestreaming.region.amazonaws.com:8443"
   # Host
   host = "transcribestreaming.region.amazonaws.com:8443"
   # Date and time of request
   amz-date = YYYYMMDD'T'HHMMSS'Z'
   # Date without time for credential scope
   datestamp = YYYYMMDD
   ```

1. Create a canonical URI\. The canonical URI is the part of the URI between the domain and the query string\.

   ```
   canonical_uri = "/stream-transcription-websocket"
   ```

1. Create the canonical headers and signed headers\. Note the trailing `"\n"` in the canonical headers\.

   ```
   canonical_headers = "host:" + host + "\n"
   signed_headers = "host"
   ```

1. Match the algorithm to the hashing algorithm\. You must use SHA\-256\.

   ```
   algorithm = "AWS4-HMAC-SHA256"
   ```

1. Create the credential scope, which scopes the derived key to the date, Region, and service to which the request is made\.

   ```
   credential_scope = datestamp + "%2f" + region + "%2f" + service + "%2f" + "aws4_request"
   ```

   `"%2f"` is the url\-encoded value of `"/"`\.

1. Create the canonical query string\. Query string values must be URL\-encoded and sorted by name\.

   ```
   canonical_querystring  = "X-Amz-Algorithm=" + algorithm
   canonical_querystring += "&X-Amz-Credential="+ access key + "%2f" + credential_scope
   canonical_querystring += "&X-Amz-Date=" + amz_date 
   canonical_querystring += "&X-Amz-Expires=300"
   canonical_querystring += "&X-Amz-Security-Token=" + token
   canonical_querystring += "&X-Amz-SignedHeaders=" + signed_headers
   canonical_querystring += "&language-code=en-US&media-encoding=pcm&sample-rate=16000"
   ```

1. Create a hash of the payload\. For a GET request, the payload is an empty string\.

   ```
   payload_hash = HashSHA256(("").Encode("utf-8")).HexDigest()
   ```

1. Combine all of the elements to create the canonical request\.

   ```
   canonical_request = method + '\n' 
      + canonical_uri + '\n' 
      + canonical_querystring + '\n' 
      + canonical_headers + '\n' 
      + signed_headers + '\n' 
      + payload_hash
   ```

**Task 2: Create the string to sign**

The string to sign contains meta information about your request\. You use the string to sign in the next step when you calculate the request signature\. For more information, see [Create a String to Sign for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-create-string-to-sign.html) in the *Amazon Web Services General Reference*\.
+ Create the string\.

  ```
  string_to_sign=algorithm + "\n"
     + amz_date + "\n"
     + credential_scope + "\n"
     + HashSHA256(canonical_request.Encode("utf-8")).HexDigest()
  ```

**Task 3: Calculate the signature**

You derive a signing key from your AWS secret access key\. For a greater degree of protection, the derived key is specific to the date, service, and AWS Region\. You use the derived key to sign the request\. For more information, see [ Calculate the Signature for AWS Signature Version 4 ](https://docs.aws.amazon.com/general/latest/gr/sigv4-calculate-signature.html) in the *Amazon Web Services General Reference*\.

The code assumes that you have implemented the `GetSignatureKey` function to derive a signing key\. For more information and example functions, see [Examples of How to Derive a Signing Key for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/signature-v4-examples.html) in the *Amazon Web Services General Reference*\.

The function `HMAC(key, data)` represents an HMAC\-SHA256 function that returns the results in binary format\.
+ Create the signing key and sign the string to sign\.

  ```
  #Create the signing key
  signing_key = GetSignatureKey(secret_key, datestamp, region, service)
                  
  # Sign the string_to_sign using the signing key
  signature = HMAC.new(signing_key, (string_to_sign).Encode("utf-8"), Sha256()).HexDigest
  ```

**Task 4: Add signing information to the request and create the request URL**

After you calculate the signature, add it to the query string\. For more information, see [Add the Signature to the Request](https://docs.aws.amazon.com/general/latest/gr/sigv4-add-signature-to-request.html) in the *Amazon Web Services General Reference*\.

1. Add the authentication information to the query string\.

   ```
   canonical_querystring += "&X-Amz-Signature=" + signature
   ```

1. Create the URL for the request\.

   ```
   request_url = endpoint + canonical_uri + "?" + canonical_querystring
   ```

You use the request URL with your WebSocket library to make the request to the Amazon Transcribe service\.

### Including WebSocket request headers<a name="websocket-headers"></a>

The request to Amazon Transcribe must include the following headers\. Typically these headers are managed by your WebSocket client library\.

```
Host: transcribestreaming.region.amazonaws.com:8443
Connection: Upgrade
Upgrade: websocket
Origin: request source
Sec-WebSocket-Version: 13
Sec-WebSocket-Key: random key
```

Use the following values for the headers:
+ **Connection** – Always `Upgrade`\.
+ **Upgrade** – Always `websocket`\.
+ **Origin** – The URI of the WebSocket client\.
+ **Sec\-WebSocket\-Version** – The version of the WebSocket protocol to use\.
+ **Sec\-WebSocket\-Key** – A base\-64 encoded randomly generated string that identifies the request\.

## Handling the WebSocket upgrade response<a name="websocket-response"></a>

When Amazon Transcribe receives your WebSocket request, it responds with a WebSocket upgrade response\. Typically your WebSocket library manages this response and sets up a socket for communications with Amazon Transcribe\.

The following is the response from Amazon Transcribe\. Line breaks have been added to the `websocket-location` header for readability\.

```
HTTP/1.1 101 Web Socket Protocol Handshake

Connection: upgrade
Upgrade: websocket
websocket-origin: wss://transcribestreaming.region.amazonaws.com:8443
websocket-location: transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket?
                   X-Amz-Algorithm=AWS4-HMAC-SHA256
                   &X-Amz-Credential=AKIDEXAMPLE%2F20190117%2Fregion%2Ftranscribe%2Faws4_request
                   &X-Amz-Date=date and time
                   &X-Amz-Expires=expiration length
                   &X-Amz-SignedHeaders=host
                   &language-code=language code
                   &media-encoding=media encoding
                   &sample-rate=media sample rate
                   &X-Amz-Signature=signature
x-amzn-RequestId: RequestId
x-amzn-SessionId: SessionId
Strict-Transport-Security: max-age=31536000
sec-websocket-accept: token
```

The response has the following values:
+ `Connection` – Always `Upgrade`\.
+ `Upgrade` – Always `websocket`\.
+ `websocket-origin` – The URI of the WebSocket server that responded to the request\.
+ `websocket-location` – The contents of the request URI that was sent to the server\. For a description of the contents, see [Creating a pre\-signed URL](#websocket-url)\.
+ `x-amzn-RequestId` – An identifier for the request\. 
+ `x-amzn-SessionId` – An identifier for a transcription session\. 
+ `Strict-Transport-Security` – A header that informs browsers to access the endpoint using only HTTPS\.
+ `sec-websocket-accept` – The hash of the `Sec-WebSocket-Key` header sent in the request\.

## Making a WebSocket streaming request<a name="websocket-streaming-request"></a>

After the WebSocket connection is established, the client can start sending a sequence of audio frames\. Each frame contains one data frame that is encoded in event stream encoding\. For more information, see [Event stream encoding](event-stream.md)\.

Each data frame contains three headers combined with a chunk of raw audio bytes\. The following table lists and describes the headers\. 


| Header name byte length | Header name \(string\) | Header value type | Value Ssring byte length | Value string \(UTF\-8\) | 
| --- | --- | --- | --- | --- | 
| 13 | :content\-type | 7 | 24 | application/octet\-stream | 
| 11 | :event\-type | 7 | 10 | AudioEvent | 
| 13 | :message\-type | 7 | 5 | event | 

To end the audio data stream, send an empty audio chunk in an event\-stream\-encoded message\.

## Handling a WebSocket streaming response<a name="websocket-streaming-response"></a>

The response contains event\-stream\-encoded raw bytes in the payload\. It contains the standard prelude and the following headers\.


| Header name byte length | Header name \(string\) | Header value type | Value string byte length | Value string \(UTF\-8\) | 
| --- | --- | --- | --- | --- | 
| 13 | :content\-type | 7 | 24 | application/octet\-stream | 
| 11 | :event\-type | 7 | 15 | TranscriptEvent | 
| 13 | :message\-type | 7 | 5 | event | 

When you decode the binary response, you end up with a JSON structure with the results of the transcription\. For an example of the JSON response, see [Streaming transcription](streaming.md)\.

## Handling WebSocket streaming errors<a name="websocket-errors"></a>

If an exception occurs while processing your request, Amazon Transcribe responds with a terminal WebSocket frame containing an event\-stream\-encoded response\. The response has the headers described in the following table, and the body of the response contains a descriptive error message\. After sending the exception response, Amazon Transcribe sends a close frame\.


| Header name byte length | Header name \(string\) | Header value type | Value string byte length | Value string \(UTF\-8\) | 
| --- | --- | --- | --- | --- | 
| 13 | :content\-type | 7 | 24 | application/octet\-stream | 
| 15 | :exception\-type | 7 | varies | varies, see below | 
| 13 | :message\-type | 7 | 9 | exception | 

The `exception-type` header contains one of the following values\.
+ `BadRequestException` – There was a client error when the stream was created, or an error occurred while streaming data\. Make sure that your client is ready to accept data and try your request again\.
+ `InternalFailureException` – Amazon Transcribe had a problem during the handshake with the client\. Try your request again\.
+ `LimitExceededException` – The client exceeded the concurrent stream limit\. For more information, see [Amazon Transcribe Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html#limits-amazon-transcribe) in the *Amazon Web Services General Reference*\. Reduce the number of streams that you are transcribing\.
+ `UnrecognizedClientException` – The WebSocket upgrade request was signed with an incorrect access key or secret key\. Make sure that you are correctly creating the access key and try your request again\.

In addition, Amazon Transcribe can return any of the common service errors\. For a list, see [Common Errors](https://docs.aws.amazon.com/transcribe/latest/dg/CommonErrors.html)\.