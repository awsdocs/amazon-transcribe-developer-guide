# Medical Custom Vocabularies<a name="how-vocabulary-med"></a>

You can give Amazon Transcribe Medical more information about how to process speech in your input file by creating one or more custom vocabularies in US English \(en\-US\)\. A *custom vocabulary* is a collection of specific words or phrases that you want Amazon Transcribe Medical to recognize in your audio input\. These vocabularies are generally domain\-specific words or phrases, words that Amazon Transcribe Medical isn't recognizing, or proper nouns\.

You can use custom vocabularies to improve the ability of Amazon Transcribe Medical to recognize a medical term\. You can also create custom vocabularies to improve its recognition of hospital names\.

Regardless of your use case, custom vocabularies work best when you use them for specific words or phrases\. We recommend that you create separate, small custom vocabularies for specific audio recordings instead of creating a single vocabulary with many terms for all your recordings\. You can have up to 100 custom vocabularies in your account\. The size limit for a custom vocabulary is 50 KB\.

You specify a custom vocabulary as a four\-column table in a text file stored in an Amazon Simple Storage Service \(Amazon S3\) bucket\. You use this file to tell Amazon Transcribe Medical how domain\-specific terms are pronounced and how to display those words in your transcriptions\.

To create a custom vocabulary, use the [CreateMedicalVocabulary](API_CreateMedicalVocabulary.md) operation or the [Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\. After you submit the  request to create a custom vocabulary, Amazon Transcribe Medical processes it\. To see the processing status of the vocabulary, use the console or the [GetMedicalVocabulary](API_GetMedicalVocabulary.md) operation\.

To use the custom vocabulary with the API, set the `VocabularyName` field of the `Settings` request parameter when you call the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation\.

## Create a Medical Custom Vocabulary<a name="create-vocabulary-table-med"></a>

You create a custom vocabulary by creating a table in a text file\. Each row in the table contains four columns\. You must enter a value in the `Phrase` column\. You have the option to leave the `IPA`, `SoundsLike`, and `DisplayAs` columns blank\. Each column must contain:
+ Fewer than 256 characters, including hyphens
+ Only characters from the allowed character set, see [Character Sets for Amazon Transcribe Medical](#charsets-med)

Place each word or phrase in your text file on a separate line\. Separate the columns with Tab characters\. Include spaces only for values in the `IPA` and `DisplayAs` columns\. Save the file with the extension `.txt` in an S3 bucket in the same AWS Region that you are calling the API or using the console\. 

If you edit your text file in Windows, make sure that your file is in `LF` format and not in `CRLF` format\. Otherwise, you will be unable to create your custom vocabulary\. Some text editors enable you to change the formatting with Find and Replace commands\.

The following examples show text that you can use to create custom vocabularies\. To create a custom vocabulary from these examples, copy an example into a text editor, replace `[TAB]` with a Tab character, and upload the saved text file to Amazon S3\.

```
Phrase[TAB]IPA[TAB]SoundsLike[TAB]DisplayAs
acute-respiratory-distress-syndrome[TAB][TAB][TAB]acute respiratory distress syndrome
A.L.L.[TAB]eɪ ɛ l ɛ l[TAB][TAB]ALL
atrioventricular-nodal-reentrant-tachycardia[TAB][TAB]ay-tree-o-ven-trick-u-lar-node-al-re-entr-ant-tack-ih-card-ia[TAB]
```

You can enter columns in any order\. The following examples show other valid structures for the custom vocabulary input file\.

```
Phrase[TAB]SoundsLike[TAB]IPA[TAB]DisplayAs
acute-respiratory-distress-syndrome[TAB][TAB][TAB]acute respiratory distress syndrome
A.L.L.[TAB][TAB]eɪ ɛ l ɛ l[TAB]ALL
atrioventricular-nodal-reentrant-tachycardia[TAB]ay-tree-o-ven-trick-u-lar-node-al-re-entr-ant-tack-ih-card-ia[TAB][TAB]
```

```
DisplayAs[TAB]SoundsLike[TAB]IPA[TAB]Phrase
acute respiratory distress syndrome[TAB][TAB][TAB]acute-respiratory-distress-syndrome
ALL[TAB][TAB]eɪ ɛ l ɛ l[TAB]A.L.L.
[TAB]ay-tree-o-ven-trick-u-lar-node-al-re-entr-ant-tack-ih-card-ia[TAB][TAB]atrioventricular-nodal-reentrant-tachycardia
```

For reading ease, the following tables show the preceding examples more clearly in html format\. 


| Phrase | IPA | SoundsLike | DisplayAs | 
| --- | --- | --- | --- | 
| acute\-respiratory\-distress\-syndrome |  |  | acute respiratory distress syndrome | 
| A\.L\.L\. | eɪ ɛ l ɛ l |  | ALL | 
| atrioventricular\-nodal\-reentrant\-tachycardia |  | ay\-tree\-o\-ven\-trick\-u\-lar\-node\-al\-re\-entr\-ant\-tack\-ih\-card\-ia |  | 


| Phrase | SoundsLike | IPA | DisplayAs | 
| --- | --- | --- | --- | 
| acute\-respiratory\-distress\-syndrome |  |  | acute respiratory distress syndrome | 
| atrioventricular\-nodal\-reentrant\-tachycardia | ay\-tree\-o\-ven\-trick\-u\-lar\-node\-al\-re\-entr\-ant\-tack\-ih\-card\-ia |  |  | 
| A\.L\.L\. |  | eɪ ɛ l ɛ l | ALL | 


| DisplayAs | SoundsLike | IPA | Phrase | 
| --- | --- | --- | --- | 
| acute respiratory distress syndomre |  |  | acute\-respiratory\-distress\-syndrome | 
| ALL |  | eɪ ɛ l ɛ l | A\.L\.L\. | 
|  | ay\-tree\-o\-ven\-trick\-u\-lar\-node\-al\-re\-entr\-ant\-tack\-ih\-card\-ia |  | atrioventricular\-nodal\-reentrant\-tachycardia | 

To download a text file that contains examples that you can use to create a custom vocabulary, see [ Amazon Transcribe Medical Custom Vocabularies Examples](samples/Amazon_Transcribe_Medical_Custom_Vocabularies_Examples.zip)\. Download and unzip the file, then upload the resulting text file into your custom vocabulary\.

The columns in a custom vocabulary table include the following:
+ `Phrase` – The word or phrase that should be recognized\. You must enter values in this column\.

  If the entry is a phrase, separate the words with a hyphen \(\-\)\. For example, enter **cerebral autosomal dominant arteriopathy with subcortical infarcts and leukoencephalopathy** as **cerebral\-autosomal\-dominant\-arteriopathy\-with\-subcortical\-infarcts\-and\-leukoencephalopathy**\.

  Enter acronyms or other words whose letters should be pronounced individually as single letters followed by dots, such as **D\.N\.A\.** or **S\.T\.E\.M\.I\.**\. To enter the plural form of an acronym, such as "STEMIs," separate the "s" from the acronym with a hyphen: "**S\.T\.E\.M\.I\-s**" You can use either uppercase or lowercase letters for acronyms\.

  The `Phrase` column is required\. You can use any of the allowed characters for the input language\. For allowed characters, see [Character Sets for Amazon Transcribe Medical](#charsets-med)\. If you don't specify the `DisplayAs` column, Amazon Transcribe Medical uses the contents of the `Phrase` column in the output file\.
+ `IPA` \(column required, values can be optional\) – To specify the pronunciation of a word or phrase, you can include characters in the [International Phonetic Alphabet \(IPA\)](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet) in this column\. The `IPA` column can't contain leading or trailing spaces, and you must use a single space to separate each phoneme in the input\. For example, in English you would enter the phrase **acute\-respiratory\-distress\-syndrome** as **ə k j u t ɹ ɛ s p ɪ ɹ ə t ɔ ɹ i d ɪ s t ɹ ɛ s s ɪ n d ɹ oʊ m**\. You would enter the phrase **A\.L\.L\.** as **eɪ ɛ l ɛ l**\.

  Even if you don't specify the contents of the `IPA` column, you must include a blank `IPA` column\. If you include values in the `IPA` column, you can't provide values for the `SoundsLike` column\.

  For a list of allowed IPA characters for a specific language, see [Character Sets for Amazon Transcribe Medical](#charsets-med)\. US English is the only language available in Amazon Transcribe Medical\.
+ `SoundsLike` \(column required, values can be optional\)  – You can break a word or phrase down into smaller segments and provide a pronunciation for each segment using the standard orthography of the language to mimic the way that the word sounds\. For example, you can provide pronunciation hints for the phrase **cerebral\-autosomal\-dominant\-arteriopathy\-with\-subcortical\-infarcts\-and\-leukoencephalopathy** like this: **sir\-e\-brul\-aut\-o\-som\-ul\-dah\-mi\-nant\-ar\-ter\-ri\-o\-pa\-thy\-with\-sub\-cor\-ti\-cul\-in\-farcts\-and\-lewk\-o\-en\-ce\-phul\-ah\-pu\-thy**\. The hint for the phrase **atrioventricular\-nodal\-reentrant\-tachycardia** would look like this: **ay\-tree\-o\-ven\-trick\-u\-lar\-node\-al\-re\-entr\-ant\-tack\-ih\-card\-ia**\. You separate each part of the hint with a hyphen \(\-\)\. 

  Even if you don't provide values for the `SoundsLike` column, you must include a blank `SoundsLike` column\. If you include values in the `SoundsLike` column, you can't provide values for the `IPA` column\. 

  You can use any of the allowed characters for the input language\. For the list of allowed characters, see [Character Sets for Amazon Transcribe Medical](#charsets-med)\.
+ `DisplayAs` \(column required, values can be optional\) – Defines how the word or phrase looks when it's output\. For example, if the word or phrase is **cerebral\-autosomal\-dominant\-arteriopathy\-with\-subcortical\-infarcts\-and\-leukoencephalopathy**, you can specify the display form as `cerebral autosomal dominant arteriopathy with subcortical infarcts and leukoencephalopathy`, so that the hyphen is not present\. You can also specify `DisplayAs` as `CADASIL` if you'd like to show the acronym instead of the full term in the output\.

  If you don't specify the `DisplayAs` column, Amazon Transcribe Medical uses the `Phrase` column from the input file in the output\.

  You can use any UTF\-8 character in the `DisplayAs` column\.

## Character Sets for Amazon Transcribe Medical<a name="charsets-med"></a>

To use Amazon Transcribe Medical's custom vocabularies, use the following character sets\.

## English Character Set<a name="char-english"></a>

For English custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` columns:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can use the following International Phonetic Alphabet \(IPA\) characters in the `IPA` column of the vocabulary input file\.


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| aʊ | 0061 028A | w | 0077 | 
| aɪ | 0061 026A | z | 007A | 
| b | 0062 | æ | 00E6 | 
| d | 0064 | ð | 00F0 | 
| eɪ | 0065 026A | ŋ | 014B | 
| f | 0066 | ɑ | 0251 | 
| g | 0067 | ɔ | 0254 | 
| h | 0068 | ɔɪ | 0254 026A | 
| i | 0069 | ə | 0259 | 
| j | 006A | ɛ | 025B | 
| k | 006B | ɝ | 025D | 
| l | 006C | ɡ | 0261 | 
| l̩ | 006C 0329 | ɪ | 026A | 
| m | 006D | ɹ | 0279 | 
| n | 006E | ʃ | 0283 | 
| n̩ | 006E 0329 | ʊ | 028A | 
| oʊ | 006F 028A | ʌ | 028C | 
| p | 0070 | ʍ | 028D | 
| s | 0073 | ʒ | 0292 | 
| t | 0074 | ʤ | 02A4 | 
| u | 0075 | ʧ | 02A7 | 
| v | 0076 | θ | 03B8 | 