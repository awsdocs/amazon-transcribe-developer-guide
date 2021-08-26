# Custom vocabularies<a name="how-vocabulary"></a>

You can give Amazon Transcribe more information about how to process speech in your input file by creating a custom vocabulary in text file format\. A *custom vocabulary* is a list of specific words that you want Amazon Transcribe to recognize in your audio input\. These are generally domain\-specific words and phrases, words that Amazon Transcribe isn't recognizing, or proper nouns\.

**Important**  
You are responsible for the integrity of your own data when you use Amazon Transcribe\. Do not enter confidential information, personal information \(PII\), or protected health information \(PHI\) into a custom vocabulary\.

Custom vocabularies work best when used to target specific words or phrases\. We recommend you create separate small vocabularies tailored to specific audio recordings instead of creating a single, large vocabulary for use with all of your recordings\.

Custom vocabulary basics:
+ You can have up to 100 vocabularies \(as separate text files\) in your account\.
+ The size limit for each custom vocabulary file is 50 Kb\.
+ Each vocabulary file can be in either table or list format; table format is strongly recommenended\.
+ Your vocabulary files must be stored in an S3 bucket if using a table format\. If using a list, you can upload a text file using the console or include your list of words within an API/CLI call\.
+ Each entry must contain fewer than 256 characters, including hyphens\.
+ Only use characters from the allowed character set for your language \(see [Character sets for custom vocabularies](charsets.md)\)\.
+ If an entry in the list is a phrase, you must separate the words of the phrase with a hyphen\. For example, if the phrase is **Los Angeles**, you would enter it in the file as **Los\-Angeles**\.

**Why use a table instead of a list for your custom vocabulary?**

The table format gives you more options for—and more control over—the input and output of words within your custom vocabulary\. The console, API, and CLI all use custom vocabulary tables in the same way; lists are used differently for each method and may require additional formatting\-related steps for successful use between the console, API, and CLI\.

To create a custom vocabulary, use the [CreateVocabulary](API_CreateVocabulary.md) API or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. After you submit the [CreateVocabulary](API_CreateVocabulary.md) request, Amazon Transcribe processes the vocabulary\. To see the processing status of the vocabulary, use the console or the [GetVocabulary](API_GetVocabulary.md) API\.

To use the custom vocabulary, set the `VocabularyName` field of the `Settings` field when you call the [StartTranscriptionJob](API_StartTranscriptionJob.md) API or choose the vocabulary in the console when you create the transcription job\. 

## Using acronyms in your custom vocabulary<a name="create-vocabulary-acronym"></a>

Enter acronyms, or other words whose letters should be pronounced individually, as single letters separated by periods; for example: **A\.B\.C\.**, **F\.B\.I\.**, **A\.W\.S\.**\. To enter the plural form of an acronym, such as "ABCs", separate the "s" from the acronym with a hyphen: **A\.B\.C\.\-s**\. You can use upper or lower case letters to define an acronym\. Acronyms are not supported in all languages; refer to [Supported languages and language\-specific features](how-it-works.md#table-language-matrix)\.

## Create a custom vocabulary using a table<a name="create-vocabulary-table"></a>

You can create a custom vocabulary by creating a four\-column table in a text file with the following headers:
+ **Phrase** – The word or phrase that should be recognized\.

  If the entry is a phrase, separate the words with a hyphen \(\-\)\. For example, you type **Los Angeles** as **Los\-Angeles**\.

  Enter acronyms or other words whose letters should be pronounced individually as single letters followed by dots, such **A\.B\.C\.** or **F\.B\.I\.**\. To enter the plural form of an acronym, such as "ABCs," separate the "s" from the acronym with a hyphen: "**A\.B\.C\.\-s**"\. You can use either upper\- or lower\-case letters to enter an acronym\. For a list of languages that support acronyms, see [Supported languages and language\-specific features](how-it-works.md#table-language-matrix)\.

  The `Phrase` field is required\. You can use any of the allowed characters for the input language\. For the list of allowed characters, see the individual languages\. If you do not specify the `DisplayAs` field, Amazon Transcribe uses the contents of the `Phrase` field in the output file\.
+ **IPA** – The pronunciation of your word or phrase using IPA characters\.

  You can include characters in the [International Phonetic Alphabet \(IPA\)](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet) in this field\. The `IPA` field can't contain leading or trailing spaces, and you must use a single space to separate each phoneme in the input\. For example, in English, you would enter the phrase **Los\-Angeles** as **l ɔ s æ n ʤ ə l ə s** and **F\.B\.I\.** as **ɛ f b i aɪ**\.

  For a list of allowed IPA characters for a specific language, refer to [Character sets for custom vocabularies](charsets.md)\.
+ **SoundsLike** – The pronunciation of your word or phrase using the standard orthography of the language to mimic the way that the word sounds\.

  You can break a word or phrase down into smaller pieces \(typically based on syllables\) and provide a pronunciation for each piece based on how that piece sounds\. For example, in English, you can provide pronunciation hints for the phrase **Los\-Angeles** as **loss\-ann\-gel\-es**\. The hint for the word **Etienne** would look like this: **eh\-tee\-en**\. You separate each part of the hint with a hyphen \(\-\)\. 
+ **DisplayAs** – Defines the how the word or phrase looks when it's output\. For example, if the word or phrase is **Los\-Angeles**, you can specify the display form as "Los Angeles" so that the hyphen is not present in the output\.

  If you don't specify the `DisplayAs` field, Amazon Transcribe uses the `Phrase` field from the input file in the output\.

  You can use any UTF\-8 character in the `DisplayAs` field\.

Place each word or phrase in your text file on a separate row, separating each field with a TAB character\. Only use spaces *within* the `IPA` and `DisplayAs` columns\.

A basic custom vocabulary may look something like the following \(where **\[TAB\]** represents a TAB character\):

```
Phrase[TAB]IPA[TAB]SoundsLike[TAB]DisplayAs
Los-Angeles[TAB][TAB][TAB]Los Angeles
F.B.I.[TAB]ɛ f b i aɪ[TAB][TAB]FBI
Etienne[TAB][TAB]eh-tee-en[TAB]
```

**Important**  
In a given row, you cannot have content for both `IPA` and `SoundsLike` fields\. You must choose one or the other, or leave both fields blank; `DisplayAs` is the only required field\.

Columns can be entered in any order, as shown in the following examples\. Note that these examples use spaces to align the columns for visual clarity; however, your input files **must only** use TAB characters to separate column entries\. If you copy these examples, remove the extra spaces between columns and replace **\[TAB\]** with a TAB character\.

```
Phrase     [TAB]SoundsLike [TAB]IPA        [TAB]DisplayAs   
Los-Angeles[TAB]           [TAB]           [TAB]Los Angeles   
F.B.I      [TAB]           [TAB]ɛ f b i aɪ [TAB]FBI   
Etienne    [TAB]eh-tee-en  [TAB]           [TAB]
```

```
DisplayAs  [TAB]SoundsLike [TAB]IPA        [TAB]Phrase   
Los Angeles[TAB]           [TAB]           [TAB]Los-Angeles   
FBI        [TAB]           [TAB]ɛ f b i aɪ [TAB]F.B.I.   
           [TAB]eh-tee-en  [TAB]           [TAB]Etienne
```

Save your custom vocabulary file with the extension `.txt` in an S3 bucket in the same region where you are calling the API\. 

**Tip**  
Make sure your text file is in `LF` format\. If you use any other format, such as `CRLF`, your custom vocabulary is not accepted by Amazon Transcribe\.

## Create a custom vocabulary using a list<a name="create-vocabulary-list"></a>

You can create a custom vocabulary using a list of words or phrases in a text file\. You can place each word on its own line, or you can put multiple words on a single line, separating the words or phrases from each other with a comma\.

The list format can be uploaded as a text file when using the [ Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. If using a list with the API or CLI, you must include the list of words in the API/CLI call\. You can only use a vocabulary list stored in an S3 bucket if you are using the console\.