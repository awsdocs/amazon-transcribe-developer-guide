# StartStreamTranscription<a name="API_streaming_StartStreamTranscription"></a>

Starts a bidirectional HTTP2 stream where audio is streamed to Amazon Transcribe and the transcription results are streamed to your application\.

The following are encoded as HTTP2 headers:
+ x\-amzn\-transcribe\-language\-code
+ x\-amzn\-transcribe\-media\-encoding
+ x\-amzn\-transcribe\-sample\-rate
+ x\-amzn\-transcribe\-session\-id

For more information about using the `StartStreamTranscription` operation, see [Streaming Transcription](streaming.md)\.

## Request Syntax<a name="API_streaming_StartStreamTranscription_RequestSyntax"></a>

```
POST /stream-transcription HTTP/2
x-amzn-transcribe-language-code: LanguageCode
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-session-id: SessionId
Content-type: application/json

{
   "[AudioStream](#transcribe-streaming_StartStreamTranscription-request-AudioStream)": { 
      "[AudioEvent](API_streaming_AudioStream.md#transcribe-Type-streaming_AudioStream-AudioEvent)": { 
         "[AudioChunk](API_streaming_AudioEvent.md#transcribe-Type-streaming_AudioEvent-AudioChunk)": blob
      }
   }
}
```

## URI Request Parameters<a name="API_streaming_StartStreamTranscription_RequestParameters"></a>

The request requires the following URI parameters\.

 ** [LanguageCode](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-LanguageCode"></a>
Indicates the language used in the input audio stream\.  
Valid Values:` en-GB en-US fr-CA fr-FR es-US` 

 ** [MediaEncoding](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-MediaEncoding"></a>
The encoding used for the input audio\.   
Valid Values:` pcm` 

 ** [MediaSampleRateHertz](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the input audio\. We suggest that you use 8000 Hz for low quality audio and 16000 Hz for high quality audio\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.

 ** [SessionId](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-SessionId"></a>
A identifier for the transcription session\. Use this parameter when you want to retry a session\. If you don't provide a session ID, Amazon Transcribe will generate one for you and return it in the response\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [VocabularyName](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-VocabularyName"></a>
The name of the vocabulary to use when processing the transcription job\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

## Request Body<a name="API_streaming_StartStreamTranscription_RequestBody"></a>

The request accepts the following data as a binary stream\. For more information, see [Amazon Transcribe Streaming Format](streaming-format.md)\.

 ** [AudioStream](#API_streaming_StartStreamTranscription_RequestSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-request-AudioStream"></a>
PCM\-encoded stream of audio blobs\. The audio stream is encoded as an HTTP2 data frame\. For details of the encoding, see [Amazon Transcribe Streaming Format](streaming-format.md)\.  
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
Content-type: application/json

{
   "[TranscriptResultStream](#transcribe-streaming_StartStreamTranscription-response-TranscriptResultStream)": { 
      "[BadRequestException](API_streaming_TranscriptResultStream.md#transcribe-Type-streaming_TranscriptResultStream-BadRequestException)": { 
      },
      "[ConflictException](API_streaming_TranscriptResultStream.md#transcribe-Type-streaming_TranscriptResultStream-ConflictException)": { 
      },
      "[InternalFailureException](API_streaming_TranscriptResultStream.md#transcribe-Type-streaming_TranscriptResultStream-InternalFailureException)": { 
      },
      "[LimitExceededException](API_streaming_TranscriptResultStream.md#transcribe-Type-streaming_TranscriptResultStream-LimitExceededException)": { 
      },
      "[TranscriptEvent](API_streaming_TranscriptResultStream.md#transcribe-Type-streaming_TranscriptResultStream-TranscriptEvent)": { 
         "[Transcript](API_streaming_TranscriptEvent.md#transcribe-Type-streaming_TranscriptEvent-Transcript)": { 
            "[Results](API_streaming_Transcript.md#transcribe-Type-streaming_Transcript-Results)": [ 
               { 
                  "[Alternatives](API_streaming_Result.md#transcribe-Type-streaming_Result-Alternatives)": [ 
                     { 
                        "[Items](API_streaming_Alternative.md#transcribe-Type-streaming_Alternative-Items)": [ 
                           { 
                              "[Content](API_streaming_Item.md#transcribe-Type-streaming_Item-Content)": "string",
                              "[EndTime](API_streaming_Item.md#transcribe-Type-streaming_Item-EndTime)": number,
                              "[StartTime](API_streaming_Item.md#transcribe-Type-streaming_Item-StartTime)": number,
                              "[Type](API_streaming_Item.md#transcribe-Type-streaming_Item-Type)": "string"
                           }
                        ],
                        "[Transcript](API_streaming_Alternative.md#transcribe-Type-streaming_Alternative-Transcript)": "string"
                     }
                  ],
                  "[EndTime](API_streaming_Result.md#transcribe-Type-streaming_Result-EndTime)": number,
                  "[IsPartial](API_streaming_Result.md#transcribe-Type-streaming_Result-IsPartial)": boolean,
                  "[ResultId](API_streaming_Result.md#transcribe-Type-streaming_Result-ResultId)": "string",
                  "[StartTime](API_streaming_Result.md#transcribe-Type-streaming_Result-StartTime)": number
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

 ** [LanguageCode](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-LanguageCode"></a>
The language code for the input audio stream\.  
Valid Values:` en-US es-US` 

 ** [MediaEncoding](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-MediaEncoding"></a>
The encoding used for the input audio stream\.  
Valid Values:` pcm` 

 ** [MediaSampleRateHertz](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-MediaSampleRateHertz"></a>
The sample rate for the input audio stream\. Use 8000 Hz for low quality audio and 16000 Hz for high quality audio\.  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.

 ** [RequestId](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-RequestId"></a>
An identifier for the streaming transcription\.

 ** [SessionId](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-SessionId"></a>
An identifier for a specific transcription session\.  
Pattern: `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` 

 ** [VocabularyName](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-VocabularyName"></a>
The name of the vocabulary used when processing the job\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

The following data is returned in JSON format by the service\.

 ** [TranscriptResultStream](#API_streaming_StartStreamTranscription_ResponseSyntax) **   <a name="transcribe-streaming_StartStreamTranscription-response-TranscriptResultStream"></a>
Represents the stream of transcription events from Amazon Transcribe to your application\. For more information, see [Amazon Transcribe Streaming Format](streaming-format.md)\.  
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

## See Also<a name="API_streaming_StartStreamTranscription_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for Java](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/transcribestreaming/package-summary.html) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/TranscribeStreamingService/Client.html) 