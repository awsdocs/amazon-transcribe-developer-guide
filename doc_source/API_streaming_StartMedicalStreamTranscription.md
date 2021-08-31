# StartMedicalStreamTranscription<a name="API_streaming_StartMedicalStreamTranscription"></a>

Starts a bidirectional HTTP/2 stream where audio is streamed to Amazon Transcribe Medical and the transcription results are streamed to your application\.

## Request Syntax<a name="API_streaming_StartMedicalStreamTranscription_RequestSyntax"></a>

```
POST /medical-stream-transcription HTTP/2
x-amzn-transcribe-language-code: LanguageCode
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-specialty: Specialty
x-amzn-transcribe-type: Type
x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
x-amzn-transcribe-session-id: SessionId
x-amzn-transcribe-enable-channel-identification: EnableChannelIdentification
x-amzn-transcribe-number-of-channels: NumberOfChannels
x-amzn-transcribe-content-identification-type: ContentIdentificationType
Content-type: application/json

{
   "AudioStream": { 
      "AudioEvent": { 
         "AudioChunk": blob
      }
   }
}
```

## URI Request Parameters<a name="API_streaming_StartMedicalStreamTranscription_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [ ContentIdentificationType ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-ContentIdentificationType"></a>
Set this field to `PHI` to identify personal health information in the transcription output\.  
Valid Values:` PHI` 

 ** [ EnableChannelIdentification ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-EnableChannelIdentification"></a>
When `true`, instructs Amazon Transcribe Medical to process each audio channel separately and then merge the transcription output of each channel into a single transcription\.  
Amazon Transcribe Medical also produces a transcription of each item\. An item includes the start time, end time, and any alternative transcriptions\.  
You can't set both `ShowSpeakerLabel` and `EnableChannelIdentification` in the same request\. If you set both, your request returns a `BadRequestException`\.

 ** [ LanguageCode ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-LanguageCode"></a>
 Indicates the source language used in the input audio stream\. For Amazon Transcribe Medical, this is US English \(en\-US\)\.   
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU | it-IT | de-DE | pt-BR | ja-JP | ko-KR | zh-CN`   
Required: Yes

 ** [ MediaEncoding ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-MediaEncoding"></a>
The encoding used for the input audio\.  
Valid Values:` pcm | ogg-opus | flac`   
Required: Yes

 ** [ MediaSampleRateHertz ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-MediaSampleRateHertz"></a>
The sample rate of the input audio in Hertz\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: Yes

 ** [ NumberOfChannels ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-NumberOfChannels"></a>
The number of channels that are in your audio stream\.  
Valid Range: Minimum value of 2\.

 ** [ SessionId ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-SessionId"></a>
 Optional\. An identifier for the transcription session\. If you don't provide a session ID, Amazon Transcribe generates one for you and returns it in the response\.   
Length Constraints: Fixed length of 36\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [ ShowSpeakerLabel ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-ShowSpeakerLabel"></a>
When `true`, enables speaker identification in your real\-time stream\.

 ** [ Specialty ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-Specialty"></a>
The medical specialty of the clinician or provider\.  
Valid Values:` PRIMARYCARE | CARDIOLOGY | NEUROLOGY | ONCOLOGY | RADIOLOGY | UROLOGY`   
Required: Yes

 ** [ Type ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-Type"></a>
The type of input audio\. Choose `DICTATION` for a provider dictating patient notes\. Choose `CONVERSATION` for a dialogue between a patient and one or more medical professionanls\.  
Valid Values:` CONVERSATION | DICTATION`   
Required: Yes

 ** [ VocabularyName ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-VocabularyName"></a>
The name of the medical custom vocabulary to use when processing the real\-time stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

## Request Body<a name="API_streaming_StartMedicalStreamTranscription_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [ AudioStream ](#API_streaming_StartMedicalStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-request-AudioStream"></a>
Represents the audio stream from your application to Amazon Transcribe\.  
Type: [ AudioStream ](API_streaming_AudioStream.md) object  
Required: Yes

## Response Syntax<a name="API_streaming_StartMedicalStreamTranscription_ResponseSyntax"></a>

```
HTTP/2 200
x-amzn-request-id: RequestId
x-amzn-transcribe-language-code: LanguageCode
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-specialty: Specialty
x-amzn-transcribe-type: Type
x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
x-amzn-transcribe-session-id: SessionId
x-amzn-transcribe-enable-channel-identification: EnableChannelIdentification
x-amzn-transcribe-number-of-channels: NumberOfChannels
x-amzn-transcribe-content-identification-type: ContentIdentificationType
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
                              "StartTime": number
                           }
                        ],
                        "Items": [ 
                           { 
                              "Confidence": number,
                              "Content": "string",
                              "EndTime": number,
                              "Speaker": "string",
                              "StartTime": number,
                              "Type": "string"
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

## Response Elements<a name="API_streaming_StartMedicalStreamTranscription_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The response returns the following HTTP headers\.

 ** [ ContentIdentificationType ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-ContentIdentificationType"></a>
If the value is `PHI`, indicates that you've configured your stream to identify personal health information\.  
Valid Values:` PHI` 

 ** [ EnableChannelIdentification ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-EnableChannelIdentification"></a>
Shows whether channel identification has been enabled in the stream\.

 ** [ LanguageCode ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-LanguageCode"></a>
The language code for the response transcript\. For Amazon Transcribe Medical, this is US English \(en\-US\)\.  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU | it-IT | de-DE | pt-BR | ja-JP | ko-KR | zh-CN` 

 ** [ MediaEncoding ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-MediaEncoding"></a>
The encoding used for the input audio stream\.  
Valid Values:` pcm | ogg-opus | flac` 

 ** [ MediaSampleRateHertz ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-MediaSampleRateHertz"></a>
The sample rate of the input audio in Hertz\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.

 ** [ NumberOfChannels ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-NumberOfChannels"></a>
The number of channels identified in the stream\.  
Valid Range: Minimum value of 2\.

 ** [ RequestId ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-RequestId"></a>
An identifier for the streaming transcription\.

 ** [ SessionId ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-SessionId"></a>
Optional\. An identifier for the transcription session\. If you don't provide a session ID, Amazon Transcribe generates one for you and returns it in the response\.  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [ ShowSpeakerLabel ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-ShowSpeakerLabel"></a>
Shows whether speaker identification was enabled in the stream\.

 ** [ Specialty ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-Specialty"></a>
The specialty in the medical domain\.  
Valid Values:` PRIMARYCARE | CARDIOLOGY | NEUROLOGY | ONCOLOGY | RADIOLOGY | UROLOGY` 

 ** [ Type ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-Type"></a>
The type of audio that was transcribed\.   
Valid Values:` CONVERSATION | DICTATION` 

 ** [ VocabularyName ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-VocabularyName"></a>
The name of the vocabulary used when processing the stream\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

The following data is returned in JSON format by the service\.

 ** [ TranscriptResultStream ](#API_streaming_StartMedicalStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartMedicalStreamTranscription-response-TranscriptResultStream"></a>
Represents the stream of transcription events from Amazon Transcribe Medical to your application\.   
Type: [ MedicalTranscriptResultStream ](API_streaming_MedicalTranscriptResultStream.md) object

## Errors<a name="API_streaming_StartMedicalStreamTranscription_Errors"></a>

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

## See Also<a name="API_streaming_StartMedicalStreamTranscription_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/StartMedicalStreamTranscription) 