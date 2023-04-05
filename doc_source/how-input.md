# Data input and output<a name="how-input"></a>

Amazon Transcribe takes audio data, as a media file in an Amazon S3 bucket or a media stream, and converts it to text data\.

If you're transcribing media files stored in an Amazon S3 bucket, you're performing batch transcriptions\. If you're transcribing media streams, you're performing streaming transcriptions\. These two processes have different rules and requirements\.

With batch transcriptions, you can use [Job queueing](job-queueing.md) if you don't need to process all of your transcription jobs concurrently\. This allows Amazon Transcribe to keep track of your transcription jobs and process them when slots are available\.

**Note**  
Amazon Transcribe may temporarily store your content to continuously improve the quality of its analysis models\. See the [Amazon Transcribe FAQ](http://aws.amazon.com/transcribe/faqs/) to learn more\. To request the deletion of content that may have been stored by Amazon Transcribe, open a case with [AWS Support](http://aws.amazon.com/contact-us/)\.

## Media formats<a name="how-input-audio"></a>

Supported media types differ between batch transcriptions and streaming transcriptions, though lossless formats are recommended for both\. See the following table for details:


|  | Batch | Streaming | 
| --- | --- | --- | 
| Supported formats |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  | 
| Recommended formats |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-input.html)  | 

For best results, use a lossless format, such as FLAC or WAV with PCM 16\-bit encoding\.

**Note**  
Streaming transcriptions are not supported with all languages\. Refer to the 'Data input' column in the [supported languages table](supported-languages.md) for details\.

## Sample rates<a name="how-input-sample-rates"></a>

With batch transcription jobs, you can choose to provide a sample rate, though this parameter is optional\. If you include it in your request, make sure the value you provide matches the actual sample rate in your audio\. If you provide a sample rate that doesn't match your audio, your job may fail\.

With streaming transcriptions, you must include a sample rate in your request\. As with batch transcription jobs, make sure the value you provide matches the actual sample rate in your audio\.

Sample rates for low fidelity audio, such as telephone recordings, typically use 8,000 Hz\. For high fidelity audio, Amazon Transcribe supports values between 16,000 Hz and 48,000 Hz\.

## Output<a name="how-output"></a>

Transcription output is in JSON format\. The first part of your transcript contains the transcript itself in paragraph form, followed by additional data for every word and punctuation mark\. The data provided depends on the features you include in your request\. At a minimum, your transcript contains the start time, end time, and confidence score for every word\. The [following section](#how-it-works-output) shows example output from a basic transcription request that didn't include any additional options or features\.

All **batch transcripts** are stored in Amazon S3 buckets\. You can choose to save your transcript in your own Amazon S3 bucket, or have Amazon Transcribe use a secure default bucket\. To learn more about creating and using Amazon S3 buckets, see [Working with buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-buckets-s3.html)\.

If you want your transcript stored in an Amazon S3 bucket that you own, specify the bucket's URI in your transcription request\. Make sure you give Amazon Transcribe write permissions for this bucket before starting your batch transcription job\. If you specify your own bucket, your transcript remains in that bucket until you remove it\. 

If you don't specify an Amazon S3 bucket, Amazon Transcribe uses a secure service\-managed bucket and provides you with a temporary URI you can use to download your transcript\. Note that temporary URIs are valid for 15 minutes\. If you get an `AccessDenied` error when using the provided URI, make a `GetTranscriptionJob` request to get a new temporary URI for your transcript\.

If you opt for a default bucket, your transcript is deleted when your job expires \(90 days\)\. If you want to keep your transcript past this expiration date, you must download it\.

**Streaming transcripts** are returned via the same method you're using for your stream\.

**Tip**  
If you want to convert your JSON output into a turn\-by\-turn transcript in Word format, see this [GitHub example \(for Python3\)](https://github.com/aws-samples/amazon-transcribe-output-word-document)\. This script works with post\-call analytics transcripts and standard batch transcripts with diarization enabled\.

### Example output<a name="how-it-works-output"></a>

Transcripts provide a complete transcription in paragraph form, followed by a word\-for\-word breakdown, which provides data for every word and punctuation mark\. This includes start time, end time, a confidence score, and a type \(`pronunciation` or `punctuation`\)\.

The following example is from a simple batch transcription job that didn't include any [additional features](feature-matrix.md)\. With each additional feature that you apply to your transcription request, you get additional data in your transcript output file\.

Basic batch transcripts contain two main sections:

1. `transcripts`: Contains the entire transcript in one text block\.

1. `items`: Contains information on each word and punctuation mark from the `transcripts` section\.

Each additional feature you include in your transcription request produces additional information in your transcript\.

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