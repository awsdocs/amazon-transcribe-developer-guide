# Transcribing Numbers<a name="how-numbers"></a>

When you are transcribing US English, Australian English, British English, or Indian English audio using the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation, numbers are transcribed as digits instead of words\. For streaming transcription, numbers are transcribed as digits for US English and British English only\. For example, the spoken number "one thousand two hundred forty two" is transcribed as "1242\." 

In all other languages numbers are transcribed into their word forms\.

Numbers are transcribed according to the following rules:


| Rule | Description | 
| --- | --- | 
| Convert cardinal numbers greater than 10 to numerals | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Convert cardinal numbers followed by "million" or "billion" to numerals followed by a word when "million" or "billion" is not followed by a number\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Convert ordinal numbers greater than 10 to numbers | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Convert fractions to their numeric format\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Convert numbers less than 10 to digits if there are more than one in a row\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Decimals are indicated by "dot" or "point\." | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Convert the word "percent" after a number to a percent sign \(%\)\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Convert the words "dollar," "US dollar," "Australian dollar, "AUD," or "USD" after a number to a dollar sign \($\) before the number\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert the words "pounds," "British pounds," or "GDB" after a number to pound sign \(£\) before the number\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert the words "rupees," "Indian rupees," or "INR" after a number to rupee sign \(₹\) before the number\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html)  | 
| Convert times to numbers\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Combine years expressed as two digits into four\. Only valid for the 20th, 21st, and 22nd centuries\.  | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Convert dates to numbers\. | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 
| Separate spans of numbers by the word "to\." | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers.html) | 