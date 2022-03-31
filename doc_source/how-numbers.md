# Transcribing numbers and punctuation<a name="how-numbers"></a>

Amazon Transcribe treats numbers differently depending on the language and the context in which they're used\. For most languages, numbers are transcribed into their word forms\. English and German language variants support digit transcription, as outlined in [Rules for transcribing numbers in English](#how-numbers-english) and [Rules for transcribing numbers in German](#how-numbers-german)\.

Amazon Transcribe automatically adds punctuation to all supported languages, and capitalizes words appropriately for languages that use case distinction in their writing systems\.

For a list of supported languages, see [Supported languages and language\-specific features](supported-languages.md#table-language-matrix)\.

## Rules for transcribing numbers in English<a name="how-numbers-english"></a>

For all English language variants, numbers are transcribed according to the following rules\.


| Rule | Examples \(input audio → output text\) | 
| --- | --- | 
| Convert cardinal numbers greater than ten to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert cardinal numbers followed by "million" or "billion" to numerals followed by a word when "million" or "billion" is not followed by a number\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert ordinal numbers greater than ten to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert fractions to their numeric format\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert numbers less than ten to digits if there are more than one in a row\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| The words "dot" or "point" are displayed as a decimal\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the word "percent" after a number to a percent symbol \(%\)\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "dollar," "U S dollar," "Australian dollar, "AUD," or "USD" after a number to a dollar sign \($\) before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "pounds," "British pounds," or "GDB" after a number to pound sign \(£\) before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "rupees," "Indian rupees," or "INR" after a number to rupee sign \(₹\) before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert times to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Years expressed as two numbers are represented as four digits; this is only valid for years in the 20th, 21st, and 22nd centuries\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert dates to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Separate spans of numbers by the word "to"\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 

## Rules for transcribing numbers in German<a name="how-numbers-german"></a>

For all German language variants, numbers are transcribed according to the following rules\.


| Rule | Examples \(input audio → output text\) | 
| --- | --- | 
| Convert cardinal numbers greater than ten to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert cardinal numbers followed by "million" or "billion" to numerals followed by a word when "million" or "billion" is not followed by a number\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert ordinal numbers greater than ten to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Fractions are not converted into a numeric format\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert numbers less than ten to digits if there are more than one in a row\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Decimals are indicated by ","\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the word "percent" after a number to a percent symbol \(%\)\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert the words "Euro" to a euro sign\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Convert times to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert dates to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Display slashes and dashes\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
|  Display numbered paragraphs\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 