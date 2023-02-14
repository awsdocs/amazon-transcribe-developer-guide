# Creating a text file for your medical custom vocabulary<a name="create-med-vocab-text"></a>

To create a custom vocabulary, you create a text file that is in UTF\-8 format\. In this file, you create a four column table, with each column specifying a field\. Each field tells Amazon Transcribe Medical either how the domain\-specific terms are pronounced or how to display these terms in your transcriptions\. You store the text file containing these fields in an Amazon S3 bucket\.

## Understanding how to format your text file<a name="understand-vocab-formatting"></a>

To create a medical custom vocabulary, you enter the column names as a header row\. You enter the values for each column beneath the header row\.

The following are the names of the four columns of the table:
+  `Phrase` – column required, values required 
+  `IPA` – column required, values can be optional 
+  `SoundsLike` – column required, values can be optional 
+  `DisplayAs` – column required, values can be optional 

When you create a custom vocabulary, make sure that you:
+ Separate each column with a single Tab character\. Amazon Transcribe throws an error message if you try to separate the columns with spaces or multiple Tab characters\.
+ Make sure that there's no trailing spaces or white space after each value within a column\.

Make sure that the values that you enter for each column:
+ Have fewer than 256 characters, including hyphens
+ Use only characters from the allowed character set, see [Character set for Amazon Transcribe Medical](charsets-med.md)\.

## Entering values for the columns of the table<a name="entering-vocabulary-values-med"></a>

The following information shows you how to specify values for the four columns of the table:
+ `Phrase` – The word or phrase that should be recognized\. You must enter values in this column\.

  If the entry is a phrase, separate the words with a hyphen \(\-\)\. For example, enter **cerebral autosomal dominant arteriopathy with subcortical infarcts and leukoencephalopathy** as **cerebral\-autosomal\-dominant\-arteriopathy\-with\-subcortical\-infarcts\-and\-leukoencephalopathy**\.

  Enter acronyms or other words whose letters should be pronounced individually as single letters followed by dots, such as **D\.N\.A\.** or **S\.T\.E\.M\.I\.**\. To enter the plural form of an acronym, such as "STEMIs," separate the "s" from the acronym with a hyphen: "**S\.T\.E\.M\.I\-s**" You can use either uppercase or lowercase letters for acronyms\.

  The `Phrase` column is required\. You can use any of the allowed characters for the input language\. For allowed characters, see [Character set for Amazon Transcribe Medical](charsets-med.md)\. If you don't specify the `DisplayAs` column, Amazon Transcribe Medical uses the contents of the `Phrase` column in the output file\.
+ `IPA` \(column required, values can be optional\) – To specify the pronunciation of a word or phrase, you can include characters in the [International Phonetic Alphabet \(IPA\)](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet) in this column\. The `IPA` column can't contain leading or trailing spaces, and you must use a single space to separate each phoneme in the input\. For example, in English you would enter the phrase **acute\-respiratory\-distress\-syndrome** as **ə k j u t ɹ ɛ s p ɪ ɹ ə t ɔ ɹ i d ɪ s t ɹ ɛ s s ɪ n d ɹ oʊ m**\. You would enter the phrase **A\.L\.L\.** as **eɪ ɛ l ɛ l**\.

  Even if you don't specify the contents of the `IPA` column, you must include a blank `IPA` column\. If you include values in the `IPA` column, you can't provide values for the `SoundsLike` column\.

  For a list of allowed IPA characters for a specific language, see [Character set for Amazon Transcribe Medical](charsets-med.md)\. US English is the only language available in Amazon Transcribe Medical\.
+ `SoundsLike` \(column required, values can be optional\) – You can break a word or phrase down into smaller segments and provide a pronunciation for each segment using the standard orthography of the language to mimic the way that the word sounds\. For example, you can provide pronunciation hints for the phrase **cerebral\-autosomal\-dominant\-arteriopathy\-with\-subcortical\-infarcts\-and\-leukoencephalopathy** like this: **sir\-e\-brul\-aut\-o\-som\-ul\-dah\-mi\-nant\-ar\-ter\-ri\-o\-pa\-thy\-with\-sub\-cor\-ti\-cul\-in\-farcts\-and\-lewk\-o\-en\-ce\-phul\-ah\-pu\-thy**\. The hint for the phrase **atrioventricular\-nodal\-reentrant\-tachycardia** would look like this: **ay\-tree\-o\-ven\-trick\-u\-lar\-node\-al\-re\-entr\-ant\-tack\-ih\-card\-ia**\. You separate each part of the hint with a hyphen \(\-\)\. 

  Even if you don't provide values for the `SoundsLike` column, you must include a blank `SoundsLike` column\. If you include values in the `SoundsLike` column, you can't provide values for the `IPA` column\. 

  You can use any of the allowed characters for the input language\. For the list of allowed characters, see [Character set for Amazon Transcribe Medical](charsets-med.md)\.
+ `DisplayAs` \(column required, values can be optional\) – Defines how the word or phrase looks when it's output\. For example, if the word or phrase is **cerebral\-autosomal\-dominant\-arteriopathy\-with\-subcortical\-infarcts\-and\-leukoencephalopathy**, you can specify the display form as `cerebral autosomal dominant arteriopathy with subcortical infarcts and leukoencephalopathy`, so that the hyphen is not present\. You can also specify `DisplayAs` as `CADASIL` if you'd like to show the acronym instead of the full term in the output\.

  If you don't specify the `DisplayAs` column, Amazon Transcribe Medical uses the `Phrase` column from the input file in the output\.

  You can use any UTF\-8 character in the `DisplayAs` column\.

You can include spaces only for the values in the `IPA` and `DisplayAs` columns\.

To create the text file of your custom vocabulary, place each word or phrase in your text file on a separate line\. Separate the columns with Tab characters\. Include spaces only for values in the `IPA` and `DisplayAs` columns\. Save the file with the extension `.txt` in an Amazon S3 bucket in the same AWS Region where you use Amazon Transcribe Medical to create your custom vocabulary\.

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

For reading ease, the following tables show the preceding examples more clearly in html format\. They are meant only to illustrate the examples\.


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
| acute respiratory distress syndrome |  |  | acute\-respiratory\-distress\-syndrome | 
| ALL |  | eɪ ɛ l ɛ l | A\.L\.L\. | 
|  | ay\-tree\-o\-ven\-trick\-u\-lar\-node\-al\-re\-entr\-ant\-tack\-ih\-card\-ia |  | atrioventricular\-nodal\-reentrant\-tachycardia | 