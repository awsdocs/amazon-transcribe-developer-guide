# Partial result stabilization<a name="result-stabilization"></a>

Amazon Transcribe starts returning transcription results as soon as you start streaming your audio\. It returns these *partial results* incrementally until it generates a finalized result at the level of a natural speech segment\. A natural speech segment is continuous speech that is broken up by a pause in the audio, or a change in speaker\. For each speech segment, any word or phrase in these partial results might change\. Amazon Transcribe continues outputting partial results until it generates the final transcription result for a speech segment\. 

You can use partial result stabilization to generate partial transcription results that are less likely to change\.  If you activate partial result stabilization, only the last few words from the partial results can change\. 

Turning on partial result stabilization changes how Amazon Transcribe produces the final transcription results\. Because only the last few words can change between the partial results, activating partial result stabilization might impact the transcription accuracy\. 

Partial result stabilization reduces the time it takes to present the transcription results\. Partial result stabilization also gives you the option to change the amount of text that you want to display\. You can use partial result stabilization in either your HTTP/2 or WebSocket streams\.

When you start a stream with Amazon Transcribe, you have two options for each speech segment:
+ Wait for the finalized results\.
+ Use the partial results in the transcription output

Using partial results reduces latency\. This reduction in latency could be helpful for use cases such as subtitling videos or generating captions for live streams\. You can use partial result stabilization to present the transcription results to your viewers more quickly\.

With partial result stabilization, you can choose the part of the transcription output that won't change\. You can also use it to present viewers with subtitles that are easier to read\. By displaying partial results, you also limit the amount of text displayed at a given time\.

The following text shows how the transcription output might change as Amazon Transcribe processes a stream when partial result stabilization isn't activated\. The last line represents the finalized result\. The lines before that one represent the partial results\.

```
            And if you held onto the ships
            and if you held onto the shift
            and if you hold onto the shift key
            and if you hold onto the shift keys
```

The following text shows how the transcription output might change as Amazon Transcribe processes a stream when partial result stabilization is activated\. The last line represents the finalized result\. The lines before that one represent the partial results\.

```
            and if you hold onto the ships
            and if you hold onto the shift
            and if you hold onto the shift key
            and if you hold onto the shift keys
```

In addition to turning on partial result stabilization, you can also change the stability level of the transcription results\. The stability level determines how stable you want the transcription results to be\. A higher stability level means that the transcription results that Amazon Transcribe returns are less likely to change\. This setting comes with lower overall transcription accuracy than the accuracy of a lower stability level\. A lower stability level results in more accurate transcription results, but those results are more likely to change\.

## Using partial result stabilization in an HTTP/2 request<a name="stabilization-http2"></a>

The following is the syntax for the parameters of an HTTP/2 request with partial result stabilization activated\.

```
POST /stream-transcription HTTP/2
x-amzn-transcribe-language-code: LanguageCode
x-amzn-transcribe-sample-rate: MediaSampleRateHertz
x-amzn-transcribe-media-encoding: MediaEncoding
x-amzn-transcribe-vocabulary-name: VocabularyName
x-amzn-transcribe-session-id: SessionId
x-amzn-transcribe-vocabulary-filter-name: VocabularyFilterName
x-amzn-transcribe-vocabulary-filter-method: VocabularyFilterMethod
x-amzn-transcribe-language-model-name: LanguageModelName
x-amzn-transcribe-enable-channel-identification: EnableChannelIdentification
x-amzn-transcribe-number-of-channels: NumberOfChannels
x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
x-amzn-transcribe-enable-partial-results-stabilization: EnablePartialResultsStabilization
x-amzn-transcribe-partial-results-stability: PartialResultsStability
Content-type: application/json
```

To activate partial result stabilization in an HTTP/2 stream, use the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation and specify the following:
+ `LanguageCode` – The language code that corresponds to the language spoken in the stream\. For a list of languages available in streaming transcription, see [What is Amazon Transcribe?](transcribe-whatis.md)\.
+ `MediaSampleHertz` – The sample rate of the audio\.
+ `EnablePartialResultsStabilization` – `true`\.
+ `PartialResultsStability` \(optional\) – The stability level of the transcription results\. Valid values are `high`, `medium`, and `low`\. Between the stability levels, the `high` stability level has partial results are least likely to change as the stream progresses\. The `low` stability level shows partial results that are the most likely to change as the stream progresses, but those results have the highest overall accuracy\. If you don't specify a value, Amazon Transcribe uses `high`\.

## Using partial result stabilization with WebSocket streams<a name="stabilization-websocket"></a>

To use partial result stabilization in WebSocket streams, use the following format to create a pre\-signed URL to start a WebSocket request and specify the following:

```
GET wss://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket
?language-code=languageCode
    &X-Amz-Algorithm=AWS4-HMAC-SHA256
    &X-Amz-Credential=Signature Version 4 credential scope
    &X-Amz-Date=date
    &X-Amz-Expires=time in seconds until expiration
    &X-Amz-Security-Token=security-token
    &X-Amz-Signature=Signature Version 4 signature
    &X-Amz-SignedHeaders=host
    &media-encoding=mediaEncoding
    &sample-rate=mediaSampleRateHertz
    &session-id=sessionId
    &enable-partial-results-stabilization=true
    &partial-results-stability=stability-level
```

 A pre\-signed URL contains the information to set up bi\-directional communication between your application and Amazon Transcribe\.

To activate partial result stabilization, you specify the following parameters:
+ `enable-partial-results-stabilization` – `true`
+ `partial-results-stability` \(optional\) – The stability level of the transcription results\. Valid values are `high`, `medium`, and `low`\. Between the stability levels, the `high` stability level has partial results are least likely to change as the stream progresses\. The `low` stability level shows partial results that are the most likely to change as the stream progresses, but those results have the highest overall accuracy\. If you don't specify a value, Amazon Transcribe uses `high`\.

For more information about completing WebSocket requests, see [Creating a pre\-signed URL](websocket.md#websocket-url)\.

## Streaming transcription output<a name="stabilization-output"></a>

The following is an example response for a streaming request with metadata removed for clarity\.

```
"Transcript": {
            "Results": [
                {
                ...
                    "Alternatives": [
                        {
                            "Items": [
                            ...
                                {
                                    "Content": "and",
                                    "EndTime": 1.02,
                                    "StartTime": 0.98,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": false,
                                    "Stable": true
                                },
                                {
                                    "Content": "if",
                                    "EndTime": 1.26,
                                    "StartTime": 1.03,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": false,
                                    "Stable": true
                                },
                                {
                                    "Content": "you",
                                    "EndTime": 1.41,
                                    "StartTime": 1.27,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": false,
                                    "Stable": true
                                },
                                {
                                    "Content": "hold",
                                    "EndTime": 1.81,
                                    "StartTime": 1.42,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": true,
                                    "Stable": true
                                },
                                {
                                    "Content": "onto",
                                    "EndTime": 2.11,
                                    "StartTime": 1.82,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": true,
                                    "Stable": true
                                },
                                {
                                    "Content": "the",
                                    "EndTime": 2.32,
                                    "StartTime": 2.12,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": true,
                                    "Stable": true
                                },
                                {
                                    "Content": "shift",
                                    "EndTime": 2.56,
                                    "StartTime": 2.33,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": true,
                                    "Stable": true
                                }
                                {
                                    "Content": "key",
                                    "EndTime": 2.81,
                                    "StartTime": 2.57,
                                    "Type": "pronunciation",
                                    "VocabularyFilterMatch": true,
                                    "Stable": false
                                }
                                ...
                                ]
                                }
                                    ]
                                        }
                                           ]
                                               }
```

When you activate partial result stabilization, Amazon Transcribe uses the `Stable` field to indicate whether the *item* is stable\. An item is a transcribed word or phrase\. You can use the `Stable` field to include or remove items that aren't stable between the stability levels, the `high` stability level has partial results are least likely to change as the stream progresses\. The `low` stability level shows partial results that are the most likely to change as the stream progresses, but those results have the highest overall accuracy\. 