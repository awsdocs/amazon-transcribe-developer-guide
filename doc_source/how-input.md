# Data input and output<a name="how-input"></a>

Amazon Transcribe takes audio data, either a media file in an Amazon S3 bucket or a media stream, and converts it to text data\.

If you're working with media files stored in an Amazon S3 bucket, you're performing batch transcription jobs; if you're working with media streams, you're performing streaming transcriptions\. These two processes have different rules and requirements\.

## Media formats<a name="how-input-audio"></a>

Supported media types differ between batch transcriptions and streaming transcriptions, though lossless formats are recommended for both\. See the following table for details:


|  | Batch | Streaming | 
| --- | --- | --- | 
| Supported formats |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  | 
| Recommended formats |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  | 

**Note**  
Streaming transcriptions are not supported with all languages\. Refer to the 'Data input' column in the [supported languages table](supported-languages.md) for details\.

## Sample rates<a name="how-input-sample-rates"></a>

With batch transcription jobs, you can choose to provide a sample rate, though this parameter is optional\. If you do include it in your request, make sure the value you provide matches the actual sample rate in your audio; if you provide a sample rate that doesn't match your audio, your job may fail\.

With streaming transcriptions, you must include a sample rate in your request\. As with batch transcription jobs, make sure the value you provide matches the actual sample rate in your audio\.

Sample rates for low fidelity audio, such as telephone recordings, typically use 8,000 Hz\. For high fidelity audio, Amazon Transcribe supports values between 16,000 Hz and 48,000 Hz\.

## Output<a name="how-output"></a>

Transcription output is in JSON format\. The first part of your transcript contains the transcript itself, in paragraph form, followed by additional data for every word and punctuation mark\. The data provided depends on the features you include in your request\. At a minimum, your transcript contains the start time, end time, and confidence score for every word\. The [following section](#how-it-works-output) shows example output from a basic transcription request that didn't include any additional options or features\.

All **batch transcripts** are stored in Amazon S3 buckets\. You can either choose to save your transcript in your own Amazon S3 bucket, or have Amazon Transcribe use a secure default bucket\. To learn more about creating and using Amazon S3 buckets, see [Working with buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-buckets-s3.html)\.

If you want your transcript stored in an Amazon S3 bucket that you own, specify the bucket's URI in your transcription request\. Make sure you give Amazon Transcribe write permissions for this bucket prior to starting your batch transcription job\. If you specify your own bucket, your transcript remains in that bucket until you remove it\. 

If you don't specify an Amazon S3 bucket, Amazon Transcribe uses a secure service\-managed bucket and provides you with a temporary URI you can use to download your transcript\. Note that temporary URIs are valid for 15 minutes\. If you get an `AccessDenied` error when using the provided URI, make a `GetTranscriptionJob` request to get a new temporary URI for your transcript\.

If you opt for a default bucket, your transcript is deleted when your job expires \(90 days\)\. If you want to keep your transcript past this expiration date, you must download it\.

**Streaming transcripts** are returned via the method you're using for your stream \(WebSocket or HTTP/2\)\.

**Tip**  
If you want to convert your JSON output into a turn\-by\-turn transcript in Word format, see this [GitHub example \(for Python3\)](https://github.com/aws-samples/amazon-transcribe-output-word-document)\.

### Example output<a name="how-it-works-output"></a>

Transcripts provide you with a complete transcription in paragraph form, followed by a word\-for\-word breakdown, which provides data for every word and punctuation mark\. This includes start time, end time, a confidence score, and a type \(either `pronunciation` or `punctuation`\)\. The below example is a transcript from a simple transcription request that didn't include any [additional features](feature-matrix.md)\. With each additional feature that you apply to your transcription request, you get additional data in your transcript output file\.

```
{
    "jobName": "my-first-transcription-job",
    "accountId": "111122223333",
    "results": {
        "transcripts": [
            {
                "transcript": "Welcome to Amazon Transcribe."
            }
        ],
        "items": [
            {
                "start_time": "0.64",
                "end_time": "1.09",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "Welcome"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "1.09",
                "end_time": "1.21",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "to"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "1.21",
                "end_time": "1.74",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "Amazon"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "1.74",
                "end_time": "2.56",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "Transcribe"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "alternatives": [
                    {
                        "confidence": "0.0",
                        "content": "."
                    }
                ],
                "type": "punctuation"
            }
        ]
    },
    "status": "COMPLETED"
}
```