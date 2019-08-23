# Using Amazon Transcribe Streaming With WebSockets<a name="websocket"></a>

When you use the [WebSocket protocol](https://tools.ietf.org/html/rfc6455) to stream audio, Amazon Transcribe transcribes the stream in real time\. You encode the audio with event stream encoding, Amazon Transcribe responds with a JSON structure also encoded using event stream encoding\. For more information, see [Event Stream Encoding](event-stream.md)\. You can use this information for applications that use the WebSocket library of your choice\.

The key components of a WebSocket request to Amazon Transcribe are:
+ Creating a pre\-signed URL to access Amazon Transcribe\.
+ Creating binary WebSocket frames containing event stream encoded audio data\.
+ Handling WebSocket frames in the response\.

## IAM Policy for WebSocket Requests<a name="websocket-iam"></a>

When you use the WebSocket protocol to call Amazon Transcribe, the role that makes the request must have the following AWS Identity and Access Management policy applied\.

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

## WebSocket Request<a name="websocket-url"></a>

You construct a URL for your WebSocket request that contains the information needed to set up communication between your application and Amazon Transcribe\. The URL is in the following format\. Line breaks have been added for readability\.

```
GET https://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket
?language-code=languageCode
   &sample-rate=mediaSampleRateHertz
   &media-encoding=mediaEncoding
   &vocabulary-name=vocabularyName
   &session-id=sessionId
   &X-Amz-Security-Token=security-token
   &X-Amz-Algorithm=AWS4-HMAC-SHA256
   &X-Amz-Date=date
   &X-Amz-SignedHeaders=host
   &X-Amz-Expires=time in seconds until expiration
   &X-Amz-Credential=Signature Version 4 credential scope
   &X-Amz-Signature=Signature Version 4 signature
```

Use the following values for the URL parameters\.
+ **language\-code** – The language code for the input audio\. Valid values are `en-GB, en-US, es-US, fr-CA,` and `fr-FR`
+ **sample\-rate** – The sample rate, in Hertz, of the input audio\. We suggest that you use 8000 Hz for low\-quality audio and 16000 Hz for high\-quality audio\. The sample rate must match the sample rate in the audio file\.
+ **media\-encoding** – The encoding used for the input audio\. Must be `pcm`\.
+ **vocabulary\-name** – Optional\. The name of the vocabulary, if any, to use when processing the transcription job\.
+ **sessionId** – Optional\. An identifier for the transcription session\. If you don't provide a session ID, Amazon Transcribe will generate one for you and return it in the response\.

 The following parameters are Signature Version 4 parameters\. For more information about Signature Version 4, see [Signing AWS API Requests ](https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html) in the *Amazon Web Services General Reference*\. 
+ **X\-Amz\-Security\-Token** – Optional\. A Signature Version 4 token for temporary credentials\. If you specify the parameter, include it in the canonical query string\.
+ **X\-Amz\-Algorithm** – The algorithm you're using as part of the signing process\. For example, if you use SHA\-256 to create hashes, the value is `AWS4-HMAC-SHA256`\.
+ **X\-Amz\-Date ** – A date and time generated following the instructions in [Handling Dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html) in the *Amazon Web Services General Reference*\.
+ **X\-Amz\-SignedHeaders** – The headers that are signed when creating the signature for the request\. Always `host`\.
+ **X\-Amz\-Expires** – The length of time in seconds until the credentials expire\. The maximum value is 300 seconds \(5 minutes\)\.
+ **X\-Amz\-Credential** – The credential scope value, which is a string that includes your access key, the date, the region you are targeting, the service you are requesting, and a termination string \("aws4\_request"\)\.
+ **X\-Amz\-Signature** – The Signature Version 4 signature that you generated for the request\.

WebSocket streaming uses the Amazon Signature Version 4 process for signing requests\. Signing the request helps to verify the identity of the requester, helps to protect your audio data in transit, and protects against potential replay attacks\. For more information about Signature Version 4, see [ Signing AWS API Requests ](https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html) in the *Amazon Web Services General Reference*\.

To construct the URL for the request and create the Signature Version 4 signature, use the following steps\. The examples are shown in pseudocode\. 

**Task 1: Create a canonical request**

The first task is create a string that includes information from your request in a standardized format\. This ensures that when AWS receives the request, it can calculate the same signature that you calculated\. For more information, see [Create a Canonical Request for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-create-canonical-request.html) in the *Amazon Web Services General Reference*\.

1. Define variables for the request\.

   ```
   # HTTP verb
   method = "GET"
   # Service name
   service = "transcribe"
   # AWS Region
   region = "AWS region"
   # Amazon Transcribe streaming endpoint
   endpoint = "https://transcribe-streaming.region.amazonaws.com:8443"
   # Host
   host = "transcribe-streaming.region.amazonaws.com:8443"
   # Date and time of request
   amz-date = YYYMMDD'T'HHMMSS'Z'
   # Date without time for credential scope
   datestamp = YYYYMMDD
   ```

1. Create a canonical URI – the part of the URI between the domain to the query string\.

   ```
   canonical_uri = "/stream-transcription-websocket"
   ```

1. Create the canonical headers and signed headers\. Note the trailing "\\n" in the canonical headers\.

   ```
   canonical_headers = "host:" + host + "\n"
   signed_headers = "host"
   ```

   Match the algorithm to the hashing algorithm that you used\. You must use SHA\-256\.

   ```
   algorithm = "AWS4-HMAC-SHA256"
   ```

   Create the credential scope that scopes the derived key to the date, region, and service to which the request was made\.

   ```
   credential_scope = datestamp + "/" + region + "/" + service + "/" + "aws4_request"
   ```

1. Create the canonical query string\. Query string values must be URL\-encoded and sorted by name\.

   ```
   canonical_querystring  = "X-Amz-Algorithm=AWS4-HMAC-SHA256"
   canonical_querystring += "&X-Amz-Credentials="+ access key + "/" + credential_scope
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

1. Finally, combine all of the elements to create the canonical request\.

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
+ 

  ```
  string_to_sign=algorithm + "\n"
     + amz_date + "\n"
     + credential_scope + "\n"
     + HashSHA256(canonical_request.Encode("utf-8").HexDigest()
  ```

**Task 3: Calculate the Signature**

You derive a signing key from your AWS secret access key\. The derived key is specific to the date, service, and region for a greater degree of protection\. You then use the derived key to sign the request\. For more information, see [ Calculate the Signature for AWS Signature Version 4 ](https://docs.aws.amazon.com/general/latest/gr/sigv4-calculate-signature.html) in the *Amazon Web Services General Reference*\.

The code assumes that you have implemented a function, `GetSignatureKey`, to derive a signing key\. For more information and example functions, see [Examples of How to Derive a Signing Key for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/signature-v4-examples.html) in the *Amazon Web Services General Reference*\.

The function `HMAC(key, data)` represents an HMAC\-SHA256 function that returns the results in binary format\.
+ 

  ```
  #Create the signing key.
  signing_key = GetSignatureKey(secret_key, datestamp, region, service)
                  
  # Sign the string_to_sign using the signing key
  signature = HMAC.new(signing_key, (string_to_sign).Encode("utf-8"), Sha256()).HexDigest
  ```

**Task 4: Add signing information to the request and create the request URL**

After you calculate the signature, you add it to the query string\. For more information, see [Add the Signature to the HTTP Request](https://docs.aws.amazon.com/general/latest/gr/sigv4-add-signature-to-request.html) in the *Amazon Web Services General Reference*\.

1. Add the authentication information to the query string\.

   ```
   canonical_querystring += "&X-Amz-Signature=" + signature
   ```

1. Create the URL for the request\.

   ```
   request_url = endpoint + canonical_uri + "?" + canonical_querystring
   ```

You can use the request URL with your WebSocket library to make the request to the Amazon Transcribe service\.

### WebSocket Request Headers<a name="websocket-headers"></a>

The request to Amazon Transcribe needs to include the following headers\. Typically these headers are managed by your WebSocket client library\.

```
Host: transcribe-streaming.region.amazonaws.com:8443
Connection: Upgrade
Upgrade: websocket
Origin: request source
Sec-WebSocket-Version: 13
Sec-WebSocket-Key: random key
```

Use the following values for the headers\.
+ **Connection** – Always `Upgrade`\.
+ **Upgrade** – Always `websocket`\.
+ **Origin** – The URI of the WebSocket client\.
+ **Sec\-WebSocket\-Version** – The version of the WebSocket protocol to use\.
+ **Sec\-WebSocket\-Key** – A base\-64 encoded randomly generated string that identifies the request\.

## WebSocket Response<a name="websocket-response"></a>

Once the Amazon Transcribe service receives your WebSocket request, it responds with a WebSocket upgrade response\. Typically your WebSocket library manages this response and sets up a socket for communications with Amazon Transcribe

The following is the response from Amazon Transcribe\. Line breaks have been added to the `websocket-location` header for readability\.

```
HTTP/1.1 101 Web Socket Protocol Handshake

Connection: upgrade
Upgrade: websocket
websocket-origin: https://transcribe-streaming.region.amazonaws.com:8443
websocket-location: transcribe-streaming.region.amazonaws.com:8443/stream-transcription-websocket?
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

The response has the following values\.
+ **Connection** – Always `Upgrade`\.
+ **Upgrade** – Always `websocket`\.
+ **websocket\-origin** – The URI of the WebSocket server that responded to the request\.
+ **websocket\-location** – The contents of the request URI that was sent to the server\. For a description of the contents, see [WebSocket Request](#websocket-url)\.
+ **x\-amzn\-RequestId** – An identifier for the request\. 
+ **x\-amzn\-SessionId** – An identifier for a transcription session\. 
+ **Strict\-Transport\-Security** – A header that informs browsers to access the endpoint using only HTTPS\.
+ **sec\-websocket\-accept** – The hash of the Sec\-WebSocket\-Key header sent in the request\.

## WebSocket Streaming Request<a name="websocket-streaming-request"></a>

After the WebSocket connection is established the client can start sending a sequence of binary WebSocket frames\. Each frame contains one data frame that is encoded in event stream encoding\. For more information, see [Event Stream Encoding](event-stream.md)\.

Each data frame contains three headers combined with a chunk of raw audio bytes\. The headers are:


| Header name byte length | Header name \(string\) | Header value type | Value string byte length | Value string \(UTF\-8\) | 
| --- | --- | --- | --- | --- | 
| 13 | :content\-type | 7 | 24 | application/octet\-stream | 
| 11 | :event\-type | 7 | 10 | AudioEvent | 
| 13 | :message\-type | 7 | 5 | event | 

To end the audio data stream, send an empty audio chunk in an event stream encoded message\.

## WebSocket Streaming Response<a name="websocket-streaming-response"></a>

The response contains event stream encoded raw bytes in the payload\. It contains the standard prelude and the following headers\.


| Header name byte length | Header name \(string\) | Header value type | Value string byte length | Value string \(UTF\-8\) | 
| --- | --- | --- | --- | --- | 
| 13 | :content\-type | 7 | 24 | application/octet\-stream | 
| 11 | :event\-type | 7 | 15 | TranscriptEvent | 
| 13 | :message\-type | 7 | 5 | event | 

When you decode the binary response, you end up with a JSON structure with the results of the transcription\. For an example of the JSON response, see [Streaming Transcription](streaming.md)\.

## Error Handling<a name="websocket-errors"></a>

If an exception occurs while processing your request, Amazon Transcribe will respond with a terminal WebSocket frame containing an event stream encoded response\. The response has the following headers, and the body of the response contains a descriptive error message\. After sending the exception response, Amazon Transcribe sends a close frame\.


| Header name byte length | Header name \(string\) | Header value type | Value string byte length | Value string \(UTF\-8\) | 
| --- | --- | --- | --- | --- | 
| 13 | :content\-type | 7 | 24 | application/octet\-stream | 
| 15 | :exception\-type | 7 | varies | varies, see below | 
| 13 | :message\-type | 7 | 9 | exception | 

The `exception-type` header contains one of the following values\.
+ **BadRequestException** – There was a client error when the stream was created, or an error occurred during the stream\.
+ **InternalFailureException** – Amazon Transcribe had a problem during the handshake with the client\.
+ **LimitExceededException** – The client exceeded the concurrent stream limit\. For more information, see [Amazon Transcribe Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html#limits-amazon-transcribe) in the *Amazon Web Services General Reference*\.
+ **UnrecognizedClientException** – The WebSocket upgrade request was signed with an incorrect access key or secret key\.

In addition, Amazon Transcribe can return any of the common service errors\. For a list, see [Common Errors](https://docs.aws.amazon.com/transcribe/latest/dg/CommonErrors.html)\.