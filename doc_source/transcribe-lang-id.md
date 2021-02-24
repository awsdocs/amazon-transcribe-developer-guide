# Transcribing with automatic language identification<a name="transcribe-lang-id"></a>

You can use automatic language identification in a batch transcription job with either the Amazon Transcribe console or the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\.

## Console<a name="lang-id-console"></a>

 **To start a transcription job with automatic language identification \(console\)** 

1. Sign in to the AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](console.aws.amazon.com/transcribe)\.

1. In the navigation pane, choose **Transcription jobs**\.

1. For **Language settings**, choose **Automatic language identification**\.

1. \(Optional\) For **Language options for automatic language identification \- *optional***, choose any languages you think are present in the file that you want to transcribe\.

1. For **Input file location on S3**, under **Input data**, enter the URI of your media file, or search for it in the **Browse S3** search box\.

1. For **Data location**, under **Output data**, choose the type of S3 bucket you'd like to use to store the transcription output\.

1. Choose **Next**\.

1. Choose **Create**\.

## API<a name="lang-id-api"></a>

 **To start a transcription job with automatic language identification \(API\)** 



In the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation, specify the following:
+ For `TranscriptionJobName`, specify a name that is unique in your AWS account\.
+ In the `MediaFileUri` parameter of the `Media` object, specify the location in S3 object location of the media file that you want to transcribe\.
+ Set the `IdentifyLanguage` parameter to `true`\.
+ \(Optional\) For increased accuracy with language identification, enter an array of the languages that are spoken in your file in `LanguageOptions`\. For example, if you're confident your media file is either in US English, US Spanish, or French, provide the following array: `["en-US", "es-US", "fr-FR"]`\.



Don't specify a value for the `LanguageCode` parameter\. Doing so generates a `BadRequestException` error\.

If you specify languages for the `LanguageOptions` parameter, Amazon Transcribe shows the language codes and their associated confidence scores for the languages that you've specified in the transcription job's output\. The audio is transcribed in the language with the highest confidence score\. The following example transcription output shows that `en-GB` and `de-DE` were specified in `LanguageOptions`\.

```
{
    "jobName": "your-transcription-job",
    "accountId": "your-account-id",
    "results": {
        "language_code": "en-GB",
        "transcripts": [
            {
                "transcript": "So I see. Supposed to show some overeager squatting with an itchy trigger finger, that's who. [transcription output shortened for brevity] You know why? Why? Because I love it."
            }
        ],
        "language_identification": [
            {
                "score": "0.9883",
                "code": "en-GB"
            },
            {
                "score": "0.0117",
                "code": "de-DE"
            }
        ],
        "items": [
            {
                "start_time": "1.51",
                "end_time": "1.83",
                "alternatives": [
                    {
                        "confidence": "0.9464",
                        "content": "so"
                    }
                ],
                "type": "pronunciation"
            },
            ...
            {
                "start_time": "95.19",
                "end_time": "95.4",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "love"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "95.4",
                "end_time": "95.6",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "it"
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

If you don't specify a set of languages, the response lists the language codes and associated confidence scores of the languages that have the five highest confidence scores\. Compare the following example response with the output in the previous example\.

```
{
    ...
        "language_identification": [
            {
                "score": "0.6888",
                "code": "en-GB"
            },
            {
                "score": "0.1875",
                "code": "en-AU"
            },
            {
                "score": "0.059",
                "code": "en-IE"
            },
            {
                "score": "0.0436",
                "code": "en-AB"
            },
            {
                "score": "0.0212",
                "code": "en-US"
            }
        ],
    ...
}
```

Amazon Transcribe always transcribes audio in the language that has the highest confidence score\.

For more information about the request parameters used to start a batch transcription job and their data types, see [StartTranscriptionJob](API_StartTranscriptionJob.md)\. 

## AWS CLI<a name="lang-id-cli"></a>

To start a transcription job with automatic language identification enabled in the AWS CLI, use the following command\.

```
aws transcribe start-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET1/your-media-file.mp4 \
--identify-language \
--transcription-job-name your-transcription-job-name
```

## Finding the identified language of a transcription job<a name="view-lang-ident"></a>

To see the language code and its confidence score for a transcription job where you've identified the language, use the [GetTranscriptionJob](API_GetTranscriptionJob.md) operation \. You can retrieve this information about a transcription job during processing\. You don't need to wait for a transcription to complete to get this information\. The following AWS CLI request gets information about a specific transcription job, as shown in the example response\.

```
    aws transcribe get-transcription-job \
    --transcription-job-name your-transcription-job
```

```
{
    "TranscriptionJob": {
        "TranscriptionJobName": "your-transcription-job",
        "TranscriptionJobStatus": "COMPLETED",
        "LanguageCode": "de-DE",
        "MediaSampleRateHertz": 48000,
        "MediaFormat": "mp4",
        "Media": {
            "MediaFileUri": "s3://media-file-uri-location"
        },
        "Transcript": {
            "TranscriptFileUri": "https://transcript-file-uri-location"
        },
        "StartTime": 1599750586.471,
        "CreationTime": 1599750586.433,
        "CompletionTime": 1599751075.505,
        "Settings": {
            "ChannelIdentification": false,
            "ShowAlternatives": false
        },
        "IdentifyLanguage": true,
        "IdentifiedLanguageScore": 0.929964542388916
    }
}
```

To list the transcription jobs that have automatic language identification enabled, use the [ListTranscriptionJobs](API_ListTranscriptionJobs.md) operation\. The language that Amazon Transcribe identified is represented by its language code in the `LanguageCode` parameter in the response\. For transcription jobs with automatic language identification enabled, the `IdentifiedLanguageScore` parameter indicates how confident Amazon Transcribe is that it identified the correct language\. Its value ranges between zero and one, with zero meaning no confidence and one meaning absolute confidence\. The following AWS CLI command would return a response similar to the one that's shown\.

```
    aws transcribe list-transcription-jobs
```

```
{
    "TranscriptionJobSummaries": [
        {
            "TranscriptionJobName": "your-transcription-job",
            "CreationTime": 1598970220.096,
            "StartTime": 1598970220.14,
            "CompletionTime": 1598970276.861,
            "LanguageCode": "en-US",
            "TranscriptionJobStatus": "COMPLETED",
            "OutputLocationType": "SERVICE_BUCKET",
            "IdentifyLanguage": true,
            "IdentifiedLanguageScore": 0.8672199249267578
        }
    ]
}
```