# StartStreamTranscription<a name="API_streaming_StartStreamTranscription"></a>

Starts a bidirectional HTTP/2 stream where audio is streamed to Amazon Transcribe and the transcription results are streamed to your application\.

The following are encoded as HTTP/2 headers:
+ x\-amzn\-transcribe\-language\-code
+ x\-amzn\-transcribe\-media\-encoding
+ x\-amzn\-transcribe\-sample\-rate
+ x\-amzn\-transcribe\-session\-id

See the [ SDK for Go API Reference](https://docs.aws.amazon.com/sdk-for-go/api/service/transcribestreamingservice/#TranscribeStreamingService.StartStreamTranscription) for more detail\.

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
x-amzn-transcribe-enable-partial-results-stabilization: EnablePartialResultsStabilization
x-amzn-transcribe-partial-results-stability: PartialResultsStability
x-amzn-transcribe-content-identification-type: ContentIdentificationType
x-amzn-transcribe-content-redaction-type: ContentRedactionType
x-amzn-transcribe-pii-entity-types: PiiEntityTypes
x-amzn-transcribe-language-model-name: LanguageModelName
x-amzn-transcribe-identify-language: IdentifyLanguage
x-amzn-transcribe-language-options: LanguageOptions
x-amzn-transcribe-preferred-language: PreferredLanguage
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

 ** [ ContentIdentificationType ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-ContentIdentificationType"></a>
Set this field to PII to identify personally identifiable information \(PII\) in the transcription output\. Content identification is performed only upon complete transcription of the audio segments\.  
You can’t set both `ContentIdentificationType` and `ContentRedactionType` in the same request\. If you set both, your request returns a `BadRequestException`\.  
Valid Values:` PII` 

 ** [ ContentRedactionType ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-ContentRedactionType"></a>
Set this field to PII to redact personally identifiable information \(PII\) in the transcription output\. Content redaction is performed only upon complete transcription of the audio segments\.  
You can’t set both `ContentRedactionType` and `ContentIdentificationType` in the same request\. If you set both, your request returns a `BadRequestException`\.  
Valid Values:` PII` 

 ** [ EnableChannelIdentification ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-EnableChannelIdentification"></a>
When `true`, instructs Amazon Transcribe to process each audio channel separately, then merges the transcription output of each channel into a single transcription\.  
Amazon Transcribe also produces a transcription of each item\. An item includes the start time, end time, and any alternative transcriptions\.  
You can't set both `ShowSpeakerLabel` and `EnableChannelIdentification` in the same request\. If you set both, your request returns a `BadRequestException`\.

 ** [ EnablePartialResultsStabilization ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-EnablePartialResultsStabilization"></a>
When `true`, instructs Amazon Transcribe to present transcription results that have the partial results stabilized\. Normally, any word or phrase from one partial result can change in a subsequent partial result\. With partial results stabilization enabled, only the last few words of one partial result can change in another partial result\.

 ** [ IdentifyLanguage ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-IdentifyLanguage"></a>
Optional\. Set this value to `true` to enable language identification for your media stream\.

 ** [ LanguageCode ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-LanguageCode"></a>
The language code of the input audio stream\.  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU | it-IT | de-DE | pt-BR | ja-JP | ko-KR | zh-CN` 

 ** [ LanguageModelName ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-LanguageModelName"></a>
The name of the language model you want to use\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [ LanguageOptions ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-LanguageOptions"></a>
An object containing a list of languages that might be present in your audio\.  
You must provide two or more language codes to help Amazon Transcribe identify the correct language of your media stream with the highest possible accuracy\. You can only select one variant per language; for example, you can't include both `en-US` and `en-UK` in the same request\.  
You can only use this parameter if you've set `IdentifyLanguage` to `true`in your request\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[a-zA-Z-,]+` 

 ** [ MediaEncoding ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-MediaEncoding"></a>
The encoding used for the input audio\.  
Valid Values:` pcm | ogg-opus | flac`   
Required: Yes

 ** [ MediaSampleRateHertz ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the input audio\. We suggest that you use 8,000 Hz for low quality audio and 16,000 Hz or higher for high quality audio\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: Yes

 ** [ NumberOfChannels ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-NumberOfChannels"></a>
The number of channels that are in your audio stream\.  
Valid Range: Minimum value of 2\.

 ** [ PartialResultsStability ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-PartialResultsStability"></a>
You can use this field to set the stability level of the transcription results\. A higher stability level means that the transcription results are less likely to change\. Higher stability levels can come with lower overall transcription accuracy\.  
Valid Values:` high | medium | low` 

 ** [ PiiEntityTypes ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-PiiEntityTypes"></a>
List the PII entity types you want to identify or redact\. In order to specify entity types, you must have either `ContentIdentificationType` or `ContentRedactionType` enabled\.  
 `PIIEntityTypes` must be comma\-separated; the available values are: `BANK_ACCOUNT_NUMBER`, `BANK_ROUTING`, `CREDIT_DEBIT_NUMBER`, `CREDIT_DEBIT_CVV`, `CREDIT_DEBIT_EXPIRY`, `PIN`, `EMAIL`, `ADDRESS`, `NAME`, `PHONE`, `SSN`, and `ALL`\.  
 `PiiEntityTypes` is an optional parameter with a default value of `ALL`\.  
Length Constraints: Minimum length of 1\. Maximum length of 300\.  
Pattern: `^[A-Z_, ]+` 

 ** [ PreferredLanguage ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-PreferredLanguage"></a>
Optional\. From the subset of languages codes you provided for `LanguageOptions`, you can select one preferred language for your transcription\.  
You can only use this parameter if you've set `IdentifyLanguage` to `true`in your request\.  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU | it-IT | de-DE | pt-BR | ja-JP | ko-KR | zh-CN` 

 ** [ SessionId ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-SessionId"></a>
A identifier for the transcription session\. Use this parameter when you want to retry a session\. If you don't provide a session ID, Amazon Transcribe will generate one for you and return it in the response\.  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [ ShowSpeakerLabel ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-ShowSpeakerLabel"></a>
When `true`, enables speaker identification in your media stream\.

 ** [ VocabularyFilterMethod ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-VocabularyFilterMethod"></a>
The manner in which you use your vocabulary filter to filter words in your transcript\. `Remove` removes filtered words from your transcription results\. `Mask` masks filtered words with a `***` in your transcription results\. `Tag` keeps the filtered words in your transcription results and tags them\. The tag appears as `VocabularyFilterMatch` equal to `True`\.  
Valid Values:` remove | mask | tag` 

 ** [ VocabularyFilterName ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-VocabularyFilterName"></a>
The name of the vocabulary filter you've created that is unique to your account\. Provide the name in this field to successfully use it in a stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [ VocabularyName ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-VocabularyName"></a>
The name of the vocabulary to use when processing the transcription job\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

## Request Body<a name="API_streaming_StartStreamTranscription_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [ AudioStream ](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-AudioStream"></a>
PCM\-encoded stream of audio blobs\. The audio stream is encoded as an HTTP/2 data frame\.  
Type: [ AudioStream ](API_streaming_AudioStream.md) object  
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
x-amzn-transcribe-enable-partial-results-stabilization: EnablePartialResultsStabilization
x-amzn-transcribe-partial-results-stability: PartialResultsStability
x-amzn-transcribe-content-identification-type: ContentIdentificationType
x-amzn-transcribe-content-redaction-type: ContentRedactionType
x-amzn-transcribe-pii-entity-types: PiiEntityTypes
x-amzn-transcribe-language-model-name: LanguageModelName
x-amzn-transcribe-identify-language: IdentifyLanguage
x-amzn-transcribe-language-options: LanguageOptions
x-amzn-transcribe-preferred-language: PreferredLanguage
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
                        "Entities": [ 
                           { 
                              "Category": "string",
                              "Confidence": number,
                              "Content": "string",
                              "EndTime": number,
                              "StartTime": number,
                              "Type": "string"
                           }
                        ],
                        "Items": [ 
                           { 
                              "Confidence": number,
                              "Content": "string",
                              "EndTime": number,
                              "Speaker": "string",
                              "Stable": boolean,
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
                  "LanguageCode": "string",
                  "LanguageIdentification": [ 
                     { 
                        "LanguageCode": "string",
                        "Score": number
                     }
                  ],
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

 ** [ ContentIdentificationType ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-ContentIdentificationType"></a>
Shows whether content identification was enabled in this stream\.  
Valid Values:` PII` 

 ** [ ContentRedactionType ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-ContentRedactionType"></a>
Shows whether content redaction was enabled in this stream\.  
Valid Values:` PII` 

 ** [ EnableChannelIdentification ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-EnableChannelIdentification"></a>
Shows whether channel identification has been enabled in the stream\.

 ** [ EnablePartialResultsStabilization ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-EnablePartialResultsStabilization"></a>
Shows whether partial results stabilization has been enabled in the stream\.

 ** [ IdentifyLanguage ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-IdentifyLanguage"></a>
The language code of the language identified in your media stream\.

 ** [ LanguageCode ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-LanguageCode"></a>
The language code of the input audio stream\.  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU | it-IT | de-DE | pt-BR | ja-JP | ko-KR | zh-CN` 

 ** [ LanguageModelName ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-LanguageModelName"></a>
The name of the language model used in your media stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [ LanguageOptions ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-LanguageOptions"></a>
The language codes used in the identification of your media stream's predominant language\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[a-zA-Z-,]+` 

 ** [ MediaEncoding ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-MediaEncoding"></a>
The encoding used for the input audio stream\.  
Valid Values:` pcm | ogg-opus | flac` 

 ** [ MediaSampleRateHertz ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-MediaSampleRateHertz"></a>
The sample rate for the input audio stream\. Use 8,000 Hz for low quality audio and 16,000 Hz or higher for high quality audio\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.

 ** [ NumberOfChannels ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-NumberOfChannels"></a>
The number of channels identified in the stream\.  
Valid Range: Minimum value of 2\.

 ** [ PartialResultsStability ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-PartialResultsStability"></a>
If partial results stabilization has been enabled in the stream, shows the stability level\.  
Valid Values:` high | medium | low` 

 ** [ PiiEntityTypes ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-PiiEntityTypes"></a>
Lists the PII entity types you specified in your request\.  
Length Constraints: Minimum length of 1\. Maximum length of 300\.  
Pattern: `^[A-Z_, ]+` 

 ** [ PreferredLanguage ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-PreferredLanguage"></a>
The preferred language you specified in your request\.  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU | it-IT | de-DE | pt-BR | ja-JP | ko-KR | zh-CN` 

 ** [ RequestId ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-RequestId"></a>
An identifier for the streaming transcription\.

 ** [ SessionId ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-SessionId"></a>
An identifier for a specific transcription session\.  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [ ShowSpeakerLabel ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-ShowSpeakerLabel"></a>
Shows whether speaker identification was enabled in the stream\.

 ** [ VocabularyFilterMethod ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-VocabularyFilterMethod"></a>
The vocabulary filtering method used in the media stream\.  
Valid Values:` remove | mask | tag` 

 ** [ VocabularyFilterName ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-VocabularyFilterName"></a>
The name of the vocabulary filter used in your media stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [ VocabularyName ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-VocabularyName"></a>
The name of the vocabulary used when processing the stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

The following data is returned in JSON format by the service\.

 ** [ TranscriptResultStream ](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-TranscriptResultStream"></a>
Represents the stream of transcription events from Amazon Transcribe to your application\.  
Type: [ TranscriptResultStream ](API_streaming_TranscriptResultStream.md) object

## Errors<a name="API_streaming_StartStreamTranscription_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** BadRequestException **   
One or more arguments to the `StartStreamTranscription` or `StartMedicalStreamTranscription` operation was invalid\. For example, `MediaEncoding` was not set to a valid encoding, or `LanguageCode` was not set to a valid code\. Check the parameters and try your request again\.  
HTTP Status Code: 400

 ** ConflictException **   
A new stream started with the same session ID\. The current stream has been terminated\.  
HTTP Status Code: 409

 ** InternalFailureException **   
A problem occurred while processing the audio\. Amazon Transcribe or Amazon Transcribe Medical terminated processing\. Try your request again\.  
HTTP Status Code: 500

 ** LimitExceededException **   
You have exceeded the maximum number of concurrent transcription streams, are starting transcription streams too quickly, or the maximum audio length of 4 hours\. Wait until a stream has finished processing, or break your audio stream into smaller chunks and try your request again\.  
HTTP Status Code: 429

 ** ServiceUnavailableException **   
Service is currently unavailable\. Try your request later\.  
HTTP Status Code: 503

## See Also<a name="API_streaming_StartStreamTranscription_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/StartStreamTranscription) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/StartStreamTranscription) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/StartStreamTranscription) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/StartStreamTranscription) 