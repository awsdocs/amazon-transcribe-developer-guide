# Create a Custom Vocabulary<a name="custom-vocabulary-files"></a>

A *custom vocabulary* is a list of special words and phrases that you want Amazon Transcribe to recognize in an audio clip\. Use a custom vocabulary to help Amazon Transcribe recognize words and phrases that are common in your solution's domain\. For example, for a medical transcription solution, you might add the names of diseases and procedures\. Or you might add non\-English names, such as "Etienne"\.

## Create a Custom Vocabulary<a name="create-vocabulary"></a>

A custom vocabulary is a list of words that you want Amazon Transcribe to recognize\. Each entry in the list is a single word or phrase\. Each entry must contain:

+ fewer than 256 characters

+ only characters from the allowed character set

For valid character sets, see [English Character Set](#char-english) and [Spanish Character Set](#char-spanish)\.

The size limit for a custom vocabulary is 50 KB\.

When typing a multi\-word term or phrase into the custom vocabulary, separate the words with a hyphen \(\-\) instead of a space\. For example, type the term **IP address** as **IP\-address**\. 

Create a custom vocabulary by using the [CreateVocabulary](API_CreateVocabulary.md) operation or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe)\. If you use the Amazon Transcribe console to create a custom vocabulary, you can provide the entries in either a text file or a comma\-separated values file \(CSV\)\. 

### Creating a Custom Vocabulary with a Text File \(Console\)<a name="creating-text"></a>

When you use a text file, place each word or phrase on a separate line\. Save the file with the extension \.txt\. The following is an example input file in text format:

```
apple
bear
coffee-dog
five
earring
good-morning
hi
IPhone
Etienne
```

### Creating a Custom Vocabulary with a Comma\-separated Values File \(Console\)<a name="creating-csv"></a>

In a comma\-separated values \(CSV\) file, separate each word or phrase with a comma\. You can put multiple entries on one line, and use line returns to break long lines\. Save the file with the extension "\.csv"\. 

The following is an example input file in CSV format:

```
apple,bear,coffee-dog,
five,earring,good-morning,
hi,IPhone,Etienne
```

## English Character Set<a name="char-english"></a>

For English custom vocabularies, you can use the following characters:

+ a \- z

+ A \- Z

+ \- \(hyphen\)

## Spanish Character Set<a name="char-spanish"></a>

For Spanish custom vocabularies, you can use the following characters:

+ a \- z

+ A \- Z

+ \- \(hyphen\)

You can also use the following Unicode characters:


| Code | Character | Code | Character | 
| --- | --- | --- | --- | 
| 00C1 | Á | 00E1 | á | 
| 00C9 | É | 00E9 | é | 
| 00CD | Í | 00ED | í | 
| 00D3 | Ó | 0XF3 | ó | 
| 00DA | Ú | 00FA | ú | 
| 00D1 | Ñ | 0XF1 | ñ | 
| 00FC | ü |   |   | 