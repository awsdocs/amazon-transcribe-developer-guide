# Sentiment analysis<a name="call-analytics-sentiment"></a>

Sentiment analysis estimates how the customer and agent are feeling throughout the call\. This metric is represented as both a quantitative value \(with a range from `5` to `-5`\) and a qualitative value \(`positive`, `neutral`, or `negative`\)\. Quantitative values are provided per quarter and per call; qualitative values are provided per turn\.

Sentiment analysis works out\-of\-the\-box, and thus doesn't support customization, such as model training or custom categories\.

Using this parameter, you can quantitatively evaluate the overall sentiment for each call participant and the sentiment for each participant during each quarter of the call\. You can qualitatively evaluate turn\-by\-turn sentiment for each participant\. This metric can help identify if your agent is able to delight an upset customer by the time the call ends\.

Here's what sentiment analysis looks like in your transcription output:
+ Qualitative turn\-by\-turn sentiment values

  ```
  "Id": "Turn-ID",
  "BeginOffsetMillis": 6040,
  "EndOffsetMillis": 11650,
  "Sentiment": "NEUTRAL",
  "ParticipantRole": "CUSTOMER"
  ```
+ Quantitative sentiment values for the entire call

  ```
  "Sentiment": {
  "OverallSentiment": {
      "AGENT": 2.7,
      "CUSTOMER": 0.2
  },
  ```
+ Quantitative sentiment values per participant and per call quarter

  ```
  "SentimentByPeriod": {
          "QUARTER": {
              "AGENT": [{
                  "Score": 2.1,
                  "BeginOffsetMillis": 0,
                  "EndOffsetMillis": 69765
              }, {
                  "Score": -0.7,
                  "BeginOffsetMillis": 69765,
                  "EndOffsetMillis": 139530
              }, {
                  "Score": 5.0,
                  "BeginOffsetMillis": 139530,
                  "EndOffsetMillis": 209295
              }, {
                  "Score": 3.0,
                  "BeginOffsetMillis": 209295,
                  "EndOffsetMillis": 279060
              }],
              "CUSTOMER": [{
                  "Score": -2.0,
                  "BeginOffsetMillis": 0,
                  "EndOffsetMillis": 69660
              }, {
                  "Score": 0.0,
                  "BeginOffsetMillis": 69660,
                  "EndOffsetMillis": 139320
              }, {
                  "Score": 0.0,
                  "BeginOffsetMillis": 139320,
                  "EndOffsetMillis": 208980
              }, {
                  "Score": 2.1,
                  "BeginOffsetMillis": 208980,
                  "EndOffsetMillis": 278640
              }]
          }
      }
  }
  ```