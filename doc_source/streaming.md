# Transcribing streaming audio<a name="streaming"></a>

Using Amazon Transcribe streaming, you can produce real\-time transcriptions for your media content\. Unlike batch transcriptions, which involve uploading media files, streaming media is delivered to Amazon Transcribe in real time\. Amazon Transcribe then returns a transcript, also in real time\.

Streaming can include pre\-recorded media \(movies, music, and podcasts\) and real\-time media \(live news broadcasts\)\. Common streaming use cases for Amazon Transcribe include live closed captioning for sporting events and real\-time monitoring of call center audio\.

Streaming content is delivered as a series of sequential data packets, or 'chunks,' that Amazon Transcribe transcribes instantaneously\. The advantages to using streaming over batch include real\-time speech\-to\-text capabilities in your applications and faster transcription times\. However, this increased speed may have accuracy limitations in some cases\.

Amazon Transcribe offers the following options for streaming:
+ [AWS SDKs]()
+ [HTTP/2](streaming-http2.md)
+ [WebSockets](streaming-websocket.md)
+ [AWS Management Console](https://console.aws.amazon.com/transcribe/)

**Tip**  
We recommend using the [AWS Management Console](https://console.aws.amazon.com/transcribe) or an SDK, rather than using HTTP/2 or WebSockets directly\. If you're using your computer microphone, we suggest using the [AWS Management Console](https://console.aws.amazon.com/transcribe) for your transcription\.

Audio formats supported for streaming transcriptions are:
+ FLAC
+ OPUS\-encoded audio in an Ogg container
+ PCM \(only signed 16\-bit little\-endian audio formats, which does **not** include WAV\)

Lossless formats \(FLAC or PCM\) are recommended\.

**Note**  
Streaming transcriptions are not supported with all languages\. See [Supported languages and language\-specific features](supported-languages.md) for details\.

## Streaming and partial results<a name="streaming-partial-results"></a>

Because streaming works in real time, transcripts are produced in *partial results*\. Amazon Transcribe breaks up the incoming audio stream based on natural speech segments, such as a change in speaker or a pause in the audio\. The transcription is returned to your application in a stream of transcription events, with each response containing more transcribed speech until an entire segment is transcribed\.

An approximation of this is shown in the following code block\. You can view this process in action by signing into the [AWS Management Console](https://console.aws.amazon.com/transcribe/), selecting **Real\-time transcription**, and speaking into your microphone\. Watch the **Transcription output** pane as you speak\.

In this example, each line is the partial result of an audio segment\.

```
Welcome.
Welcome to.
Welcome to Amazon.
Welcome to Amazon transcribe.
Welcome to Amazon transcribe.
```

These partial results are present in your transcription output within the [Results](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_Result.html) objects\. Also in this object block is an **IsPartial** field\. If this field is true, your transcription segment is not yet complete\. You can view the difference between an incomplete and a complete segment below:

```
"IsPartial": true (incomplete segment)
            
"Transcript": "Welcome to Amazon."

"EndTime": 2.695,
"IsPartial": true,
"ResultId": "55421b61-7cc6-4ef1-8d55-f1c128f01d30",
"StartTime": 1.18


"IsPartial": false (complete segment)
            
"Transcript": "Welcome to Amazon transcribe."

"EndTime": 4.775,
"IsPartial": false,
"ResultId": "55421b61-7cc6-4ef1-8d55-08a97159870e",
"StartTime": 1.18
```

Each word within a complete segment has an associated confidence score, which is a value between `0` and `1`\. A larger value indicates a greater likelihood that the word is correctly transcribed\.

**Tip**  
The `StartTime` and `EndTime` of an audio segment can be used to synchronize transcription output with video dialogue\.

If you're running an application that requires low latency, you may want to use [partial\-result stabilization](#streaming-partial-result-stabilization)\.

## Partial\-result stabilization<a name="streaming-partial-result-stabilization"></a>

Amazon Transcribe starts returning transcription results as soon as you start streaming your audio\. It returns these partial results incrementally until it generates a finished result at the level of a natural speech segment\. A natural speech segment is continuous speech that contains a pause or a change in speaker\.

Amazon Transcribe continues outputting partial results until it generates the final transcription result for a speech segment\. Because speech recognition may revise words as it gains more context, streaming transcriptions can change slightly with each new partial result output\.

This process gives you two options for each speech segment:
+ Wait for the finished segment
+ Use the segment's partial results

Partial result stabilization changes how Amazon Transcribe produces the final transcription result for each complete segment\. When activated, only the last few words from the partial results can change\. Because of this, transcription accuracy may be affected\. However, your transcript is returned faster than without partial\-results stabilization\. This reduction in latency may be beneficial when subtitling videos or generating captions for live streams\.

The following examples show how the same audio stream is handled when partial\-results stabilization is not activated and when it is\. Note that you can set the stability level to low, medium, or high\. Low stability provides the highest accuracy\. High stability transcribes faster, but with slightly lower accuracy\.


| "Transcript": | "EndTime": | "IsPartial": | 
| --- | --- | --- | 
| Partial\-result stabilization not enabled | 
|  <pre>Welcome. <br />Welcome to. <br />Welcome to Amazon. <br />Welcome to Amazon.  <br />Welcome to Amazon transcribe.<br />Welcome to Amazon transcribe.<br />Welcome to Amazon transcribe. <br />Welcome to Amazon transcribe. <br />Welcome to Amazon transcribe. </pre>  |  <pre>0.515<br />1.015<br />1.515 <br />2.015<br />2.515<br />3.015<br />3.515<br />3.595<br />3.595</pre>  |  <pre>true<br />true<br />true<br />true<br />true<br />true<br />true<br />true<br />false</pre>  | 
| Partial\-result stabilization enabled \(high stability\) | 
|  <pre>Welcome. <br />Welcome to<br />Welcome to Amas.<br />Welcome to Amazon.  <br />Welcome to Amazon.<br />Welcome to Amazon transcribe.<br />Welcome to Amazon transcribe.</pre>  |  <pre>0.515<br />1.015<br />1.515<br />2.015<br />2.515<br />2.865<br />2.865</pre>  |  <pre>true<br />true<br />true<br />true<br />true<br />true<br />false</pre>  | 

When you activate partial\-result stabilization, Amazon Transcribe uses a `Stable` field to indicate whether an item is stable, where 'item' refers to a transcribed word or phrase\. Values for `Stable` are either `true`, indicating that the item is stable, or `false`, indicating that the item is not stable\. Items flagged as `false` \(not stable\) are more likely to change as your segment is transcribed\. Conversely, items flagged as `true` \(stable\) don't change\.

You can choose to render non\-stable words so your captions align with speech\. Even if captions change slightly as context is added, this is a better user experience than periodic text bursts, which may or may not align with speech\.

You can also choose to display non\-stable words in a different format, such as italics, to indicate to viewers that these words may change\. Displaying partial results limits the amount of text displayed at a given time\. This can be important when you're dealing with space constraints, as with video captions\.

**Dive deeper with the AWS Machine Learning Blog**  
To learn more about improving accuracy with real\-time transcriptions, see:  
[Improve the streaming transcription experience with Amazon Transcribe partial results stabilization](http://aws.amazon.com/blogs/machine-learning/amazon-transcribe-now-supports-partial-results-stabilization-for-streaming-audio/)
[“What was that?” Increasing subtitle accuracy for live broadcasts using Amazon Transcribe](http://aws.amazon.com/blogs/media/what-was-that-increasing-subtitle-accuracy-for-live-broadcasts-using-amazon-transcribe/)

### Partial\-result stabilization example output<a name="streaming-stabilization-output"></a>

The following example output shows `Stable` flags for an incomplete segment \(`"IsPartial": true`\)\. You can see that the words "*to Amazon*" are not stable and therefore could change before the segment is finalized\.

```
"Transcript": {
    "Results": [
        {
            "Alternatives": [
                {
                    "Items": [
                        {
                            "Content": "Welcome",
                            "EndTime": 2.4225,
                            "Stable": true,
                            "StartTime": 1.65,
                            "Type": "pronunciation",
                            "VocabularyFilterMatch": false
                        },
                        { 
                            "Content": "to",
                            "EndTime": 2.8325,
                            "Stable": false,
                            "StartTime": 2.4225,
                            "Type": "pronunciation",
                            "VocabularyFilterMatch": false
                        },
                        {
                            "Content": "Amazon",
                            "EndTime": 3.635,
                            "Stable": false,
                            "StartTime": 2.8325,
                            "Type": "pronunciation",
                            "VocabularyFilterMatch": false
                        },
                        {
                            "Content": ".",
                            "EndTime": 3.635,
                            "Stable": false,
                            "StartTime": 3.635,
                            "Type": "punctuation",
                            "VocabularyFilterMatch": false
                        }
                    ],
                    "Transcript": "Welcome to Amazon."
                }
            ],
            "EndTime": 4.165,
            "IsPartial": true,
            "ResultId": "364f1c74-5e21-4333-af74-b6531a6b9158",
            "StartTime": 1.65
        }
    ]
}
```