# Call characteristics<a name="call-analytics-characteristics"></a>

The call characteristics feature measures the quality of agent\-customer interactions using these metrics:
+ **Talk time**—Measures the amount of time \(in milliseconds\) each participant spoke during the call\. Use this metric to help identify if one participant is dominating the call or if the dialogue is balanced\.
+ **Non\-talk time**—Measures periods of time that do not contain speech\. Use this metric to see if there are long periods of silence, such as an agent keeping a customer on hold for an excessive amount of time\.
+ **Loudness**—Measures the volume at which each participant is speaking\. Use this metric to see if either the caller or the agent is speaking loudly or yelling, which is often indicative of being upset\. This metric is represented as a normalized value \(speech level per second of speech in a given segment\) on a scale from 0 to 100, where a higher value indicates a louder voice\.
+ **Interruption**—Measures if and when one participant cuts off the other participant mid\-sentence\. Frequent interruptions may be associated with rudeness or anger, and could correlate to negative sentiment for one or both participants\.
+ **Talk speed**—Measures the speed at which both participants are speaking\. Comprehension can be affected if one participant speaks too quickly\. This metric is measured in words per minute\.

Here's what talk time, non\-talk time, loudness scores, interruptions, and talk speed look like in your transcription output:

```
"TalkTime": {
            "DetailsByParticipant": {
                "AGENT": {
                    "TotalTimeMillis": 158120
                },
                "CUSTOMER": {
                    "TotalTimeMillis": 108009
                }
            },
            "TotalTimeMillis": 266129
        }
```

```
"NonTalkTime": {
            "Instances": [{
                "BeginOffsetMillis": 216450,
                "DurationMillis": 7690,
                "EndOffsetMillis": 224140
            }],
            "TotalTimeMillis": 7690
       },
```

```
"LoudnessScores": [
                87.87,
                85.25,
                83.46,
                81.37,
                80.37,
                75.91
            ],
```

```
"Interruptions": {
            "TotalCount": 4,
            "TotalTimeMillis": 12129,
            "InterruptionsByInterrupter": {
                "AGENT": [{
                    "BeginOffsetMillis": 30940,
                    "DurationMillis": 2800,
                    "EndOffsetMillis": 33740
                }, {
                    "BeginOffsetMillis": 133440,
                    "DurationMillis": 4510,
                    "EndOffsetMillis": 137950
                }, {
                    "BeginOffsetMillis": 163240,
                    "DurationMillis": 2710,
                    "EndOffsetMillis": 165950
                }, {
                    "BeginOffsetMillis": 169840,
                    "DurationMillis": 2110,
                    "EndOffsetMillis": 171950
                }]
            }
        },
```

```
"TalkSpeed": {
            "DetailsByParticipant": {
                "AGENT": {
                    "AverageWordsPerMinute": 195
                },
                "CUSTOMER": {
                    "AverageWordsPerMinute": 116
                }
            }
        },
```

When you're ready to set up a call analytics job, see [Start a call analytics transcription job](call-analytics-start.md)\.