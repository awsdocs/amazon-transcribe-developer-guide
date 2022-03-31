# Data input and output<a name="how-input"></a>

Amazon Transcribe takes audio data, either a media file in an S3 bucket or a media stream, and converts it to text data\.

If you're working with media files stored in an S3 bucket, you're performing batch transcription jobs; if you're working with media streams, you're performing streaming transcriptions\. These two processes have different rules and requirements\.

## Media formats<a name="how-input-audio"></a>

Supported media types differ between batch transcriptions and streaming transcriptions, though lossless formats are recommended for both\. See the following table for details:


|  | Batch | Streaming | 
| --- | --- | --- | 
| Supported formats |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  | 
| Recommended formats |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  | 

## Sample rates<a name="how-input-sample-rates"></a>

With batch transcription jobs, you can choose to provide a sample rate, though this parameter is optional\. If you do include it in your request, make sure the value you provide matches the actual sample rate in your audio; if you provide a sample rate that doesn't match your audio, your job may fail\.

With streaming transcriptions, you must include a sample rate in your request\. As with batch transcription jobs, make sure the value you provide matches the actual sample rate in your audio\.

Sample rates for low fidelity audio, such as telephone recordings, typically use 8,000 Hz\. For high fidelity audio, Amazon Transcribe supports values between 16,000 Hz and 48,000 Hz\.

## Output<a name="how-output"></a>

All batch transcripts are stored in S3 buckets\. You can either choose to save your transcript in your own S3 bucket, or have Amazon Transcribe use a secure default bucket\. To learn more about creating and using S3 buckets, see [Working with buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-buckets-s3.html)\.

If you want your transcript stored in an S3 bucket that you own, specify the bucket's URI in your transcription request\. Make sure you give Amazon Transcribe write permissions for this bucket prior to starting your batch transcription job\. If you specify your own bucket, your transcript remains in that bucket until you remove it\. 

If you don't specify an S3 bucket, Amazon Transcribe uses a secure service\-managed bucket and provides you with a temporary URI that you can use to download your transcript\. Note that temporary URIs are valid for 15 minutes\. If you get an `AccesDenied` error when using the provided URI, run a `getTranscriptionJob` request to get a new temporary URI for your transcript\.

If you opt for a default bucket, your transcript is deleted when your job expires \(90 days\)\. So if you want to keep your transcript, you must download it before the expiration date\.

Streaming transcripts are returned via the method you're using for your stream \(WebSocket or HTTP/2\)\.