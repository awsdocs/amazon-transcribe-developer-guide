# Transcribing numbers and punctuation<a name="how-numbers"></a>

Amazon Transcribe automatically adds punctuation to all the languages that it supports\. It also capitalizes words appropriately for languages that use case distinction in their writing systems\.

When using the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation, numbers are transcribed as digits instead of words for the following languages:
+ Australian English \(en\-AU\)
+ British English \(en\-GB\)
+ Indian English \(en\-IN\)
+ Irish English \(en\-IE\)
+ Scottish English \(en\-AB\)
+ US English \(en\-US\)
+ Welsh English \(en\-WL\)
+ German \(de\-DE\)
+ Swiss German \(de\-CH\)

For streaming transcription, numbers are transcribed as digits for the following languages:
+ Australian English \(en\-AU\)
+ British English \(en\-GB\)
+ US English \(en\-US\)
+ German \(de\-DE\)

For the preceding languages, the spoken number "one thousand two hundred forty\-two" is transcribed as 1242\. For all other languages, numbers are transcribed into their word forms\.

## Rules for transcribing numbers in English<a name="rules-english"></a>

For all English languages, such British English \(en\-GB\) or US English \(en\-US\), numbers are transcribed according to the following rules\. 


| Rule | Example | 
| --- | --- | 
| Convert cardinal numbers greater than 10 to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert cardinal numbers followed by "million" or "billion" to numerals followed by a word when "million" or "billion" is not followed by a number\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert ordinal numbers greater than 10 to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert fractions to their numeric format\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert numbers less than 10 to digits if there are more than one in a row\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Decimals are indicated by "dot" or "point\." |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the word "percent" after a number to a percent symbol \(%\)\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "dollar," "US dollar," "Australian dollar, "AUD," or "USD" after a number to a dollar sign \($\) before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "pounds," "British pounds," or "GDB" after a number to pound sign \(£\) before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "rupees," "Indian rupees," or "INR" after a number to rupee sign \(₹\) before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert times to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Combine years expressed as two digits into four\. Only valid for the 20th, 21st, and 22nd centuries\.   |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert dates to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Separate spans of numbers by the word "to\."  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 

## Rules for transcribing numbers in German<a name="rules-german"></a>

For German \(de\-DE\) and Swiss German \(de\-CH\), numbers are transcribed according to the following rules\. 


| Rule | Example | 
| --- | --- | 
| Convert cardinal numbers greater than 10 to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert cardinal numbers followed by "million" or "billion" to numerals followed by a word when "million" or "billion" is not followed by a number\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert ordinal numbers greater than 10 to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Fractions are not converted into a numeric format\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert numbers less than 10 to digits if there are more than one in a row\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Decimals are indicated by ","\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the word "percent" after a number to a percent symbol \(%\)\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "Euro" to a euro sign\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert times to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert dates to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Display slashes and dashes\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Display numbered paragraphs  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 