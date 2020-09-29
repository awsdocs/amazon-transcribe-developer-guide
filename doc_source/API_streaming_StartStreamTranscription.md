# StartStreamTranscription<a name="API_streaming_StartStreamTranscription"></a>

Starts a bidirectional HTTP2 stream where audio is streamed to Amazon Transcribe and the transcription results are streamed to your application\.

The following are encoded as HTTP2 headers:
+ x\-amzn\-transcribe\-language\-code
+ x\-amzn\-transcribe\-media\-encoding
+ x\-amzn\-transcribe\-sample\-rate
+ x\-amzn\-transcribe\-session\-id

## Request Syntax<a name="API_streaming_StartStreamTranscription_RequestSyntax"></a>

```
POST /stream-transcription HTTP/2
x-amzn-transcribe-language-code: LanguageCode
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-session-id: SessionId
x-amzn-transcribe-vocabulary-filter-name: VocabularyFilterName
x-amzn-transcribe-vocabulary-filter-method: VocabularyFilterMethod
x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
x-amzn-transcribe-enable-channel-identification: EnableChannelIdentification
x-amzn-transcribe-number-of-channels: NumberOfChannels
Content-type: application/json

{
   "AudioStream": { 
      "AudioEvent": { 
         "AudioChunk": blob
      }
   }
}
```

## URI Request Parameters<a name="API_streaming_StartStreamTranscription_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [EnableChannelIdentification](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-EnableChannelIdentification"></a>
When `true`, instructs Amazon Transcribe to process each audio channel separately and then merge the transcription output of each channel into a single transcription\.  
Amazon Transcribe also produces a transcription of each item\. An item includes the start time, end time, and any alternative transcriptions\.  
You can't set both `ShowSpeakerLabel` and `EnableChannelIdentification` in the same request\. If you set both, your request returns a `BadRequestException`\.

 ** [LanguageCode](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-LanguageCode"></a>
Indicates the source language used in the input audio stream\.  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU`   
Required: Yes

 ** [MediaEncoding](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-MediaEncoding"></a>
The encoding used for the input audio\.  
Valid Values:` pcm`   
Required: Yes

 ** [MediaSampleRateHertz](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the input audio\. We suggest that you use 8000 Hz for low quality audio and 16000 Hz for high quality audio\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: Yes

 ** [NumberOfChannels](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-NumberOfChannels"></a>
The number of channels that are in your audio stream\.  
Valid Range: Minimum value of 2\.

 ** [SessionId](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-SessionId"></a>
A identifier for the transcription session\. Use this parameter when you want to retry a session\. If you don't provide a session ID, Amazon Transcribe will generate one for you and return it in the response\.  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [ShowSpeakerLabel](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-ShowSpeakerLabel"></a>
When `true`, enables speaker identification in your real\-time stream\.

 ** [VocabularyFilterMethod](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-VocabularyFilterMethod"></a>
The manner in which you use your vocabulary filter to filter words in your transcript\. `Remove` removes filtered words from your transcription results\. `Mask` masks those words with a `***` in your transcription results\. `Tag` keeps the filtered words in your transcription results and tags them\. The tag appears as `VocabularyFilterMatch` equal to `True`   
Valid Values:` remove | mask | tag` 

 ** [VocabularyFilterName](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-VocabularyFilterName"></a>
The name of the vocabulary filter you've created that is unique to your AWS account\. Provide the name in this field to successfully use it in a stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyName](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-VocabularyName"></a>
The name of the vocabulary to use when processing the transcription job\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

## Request Body<a name="API_streaming_StartStreamTranscription_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [AudioStream](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-AudioStream"></a>
PCM\-encoded stream of audio blobs\. The audio stream is encoded as an HTTP2 data frame\.  
Type: [AudioStream](API_streaming_AudioStream.md) object  
Required: Yes

## Response Syntax<a name="API_streaming_StartStreamTranscription_ResponseSyntax"></a>

```
HTTP/2 200
x-amzn-request-id: RequestId
x-amzn-transcribe-language-code: LanguageCode
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-session-id: SessionId
x-amzn-transcribe-vocabulary-filter-name: VocabularyFilterName
x-amzn-transcribe-vocabulary-filter-method: VocabularyFilterMethod
x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
x-amzn-transcribe-enable-channel-identification: EnableChannelIdentification
x-amzn-transcribe-number-of-channels: NumberOfChannels
Content-type: application/json

{
   "TranscriptResultStream": { 
      "BadRequestException": { 
      },
      "ConflictException": { 
      },
      "InternalFailureException": { 
      },
      "LimitExceededException": { 
      },
      "ServiceUnavailableException": { 
      },
      "TranscriptEvent": { 
         "Transcript": { 
            "Results": [ 
               { 
                  "Alternatives": [ 
                     { 
                        "Items": [ 
                           { 
                              "Content": "string",
                              "EndTime": number,
                              "Speaker": "string",
                              "StartTime": number,
                              "Type": "string",
                              "VocabularyFilterMatch": boolean
                           }
                        ],
                        "Transcript": "string"
                     }
                  ],
                  "ChannelId": "string",
                  "EndTime": number,
                  "IsPartial": boolean,
                  "ResultId": "string",
                  "StartTime": number
               }
            ]
         }
      }
   }
}
```

## Response Elements<a name="API_streaming_StartStreamTranscription_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The response returns the following HTTP headers\.

 ** [EnableChannelIdentification](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-EnableChannelIdentification"></a>
Shows whether channel identification has been enabled in the stream\.

 ** [LanguageCode](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-LanguageCode"></a>
The language code for the input audio stream\.  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU` 

 ** [MediaEncoding](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-MediaEncoding"></a>
The encoding used for the input audio stream\.  
Valid Values:` pcm` 

 ** [MediaSampleRateHertz](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-MediaSampleRateHertz"></a>
The sample rate for the input audio stream\. Use 8000 Hz for low quality audio and 16000 Hz for high quality audio\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.

 ** [NumberOfChannels](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-NumberOfChannels"></a>
The number of channels identified in the stream\.  
Valid Range: Minimum value of 2\.

 ** [RequestId](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-RequestId"></a>
An identifier for the streaming transcription\.

 ** [SessionId](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-SessionId"></a>
An identifier for a specific transcription session\.  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [ShowSpeakerLabel](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-ShowSpeakerLabel"></a>
Shows whether speaker identification was enabled in the stream\.

 ** [VocabularyFilterMethod](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-VocabularyFilterMethod"></a>
The vocabulary filtering method used in the real\-time stream\.  
Valid Values:` remove | mask | tag` 

 ** [VocabularyFilterName](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-VocabularyFilterName"></a>
The name of the vocabulary filter used in your real\-time stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyName](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-VocabularyName"></a>
The name of the vocabulary used when processing the stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

The following data is returned in JSON format by the service\.

 ** [TranscriptResultStream](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-TranscriptResultStream"></a>
Represents the stream of transcription events from Amazon Transcribe to your application\.  
Type: [TranscriptResultStream](API_streaming_TranscriptResultStream.md) object

## Errors<a name="API_streaming_StartStreamTranscription_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
One or more arguments to the `StartStreamTranscription` operation was invalid\. For example, `MediaEncoding` was not set to `pcm` or `LanguageCode` was not set to a valid code\. Check the parameters and try your request again\.  
HTTP Status Code: 400

 **ConflictException**   
A new stream started with the same session ID\. The current stream has been terminated\.  
HTTP Status Code: 409

 **InternalFailureException**   
A problem occurred while processing the audio\. Amazon Transcribe terminated processing\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
You have exceeded the maximum number of concurrent transcription streams, are starting transcription streams too quickly, or the maximum audio length of 4 hours\. Wait until a stream has finished processing, or break your audio stream into smaller chunks and try your request again\.  
HTTP Status Code: 429

 **ServiceUnavailableException**   
Service is currently unavailable\. Try your request later\.  
HTTP Status Code: 503

## See Also<a name="API_streaming_StartStreamTranscription_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://sdk.amazonaws.com/cpp/api/LATEST/namespace_aws_1_1_transcribe_streaming_service.html) 
+  [AWS SDK for Java](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/transcribestreaming/package-summary.html) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/TranscribeStreamingService/Client.html) 