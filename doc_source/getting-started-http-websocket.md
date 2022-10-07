# Transcribing with HTTP or WebSockets<a name="getting-started-http-websocket"></a>

Amazon Transcribe supports HTTP for both batch \(HTTP/1\.1\) and streaming \(HTTP/2\) transcriptions\. WebSockets are supported for streaming transcriptions\.

If you're transcribing a media file located in an Amazon S3 bucket, you're performing a batch transcription\. If you're transcribing a real\-time stream of audio data, you're performing a streaming transcription\.

Both HTTP and WebSockets require you to authenticate your request using AWS Signature Version 4 headers\. Refer to [Signing AWS API requests](https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html) for more information\.

You can make a batch HTTP request using the following headers:
+ host
+ x\-amz\-target
+ content\-type
+ x\-amz\-content\-sha256
+ x\-amz\-date
+ authorization

Here's an example of a `StartTranscriptionJob` request:

```
POST /transcribe HTTP/1.1 
host: transcribe.us-west-2.amazonaws.com
x-amz-target: com.amazonaws.transcribe.Transcribe.StartTranscriptionJob 
content-type: application/x-amz-json-1.1
x-amz-content-sha256: string
x-amz-date: YYYYMMDDTHHMMSSZ
authorization: AWS4-HMAC-SHA256 Credential=access-key/YYYYMMSS/us-west-2/transcribe/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date;x-amz-target;x-amz-security-token, Signature=string

{
    "TranscriptionJobName": "my-first-transcription-job",
    "LanguageCode": "en-US",
    "Media": {
        "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
    },
    "OutputBucketName": "DOC-EXAMPLE-BUCKET",
    "OutputKey": "my-output-files/" 
}
```

Additional operations and parameters are listed in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\. Other signature elements are detailed in [Elements of an AWS Signature Version 4 request](https://docs.aws.amazon.com/general/latest/gr/sigv4_elements.html)\.

Streaming transcriptions using HTTP/2 and WebSockets are more complicated\. Detailed instructions are provided in these sections:
+ [Setting up an HTTP/2 stream](streaming-http2.md)
+ [Setting up a WebSocket stream](streaming-websocket.md)

We recommend reviewing the [Transcribing streaming audio](streaming.md) chapter before setting up your first HTTP/2 or WebSocket stream\.