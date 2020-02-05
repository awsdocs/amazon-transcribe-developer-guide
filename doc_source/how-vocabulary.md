# Custom Vocabularies<a name="how-vocabulary"></a>

**Topics**
+ [Create a Custom Vocabulary Using a List](#create-vocabulary-list)
+ [Create a Custom Vocabulary Using a Table](#create-vocabulary-table)
+ [Character Sets for Custom Vocabularies](#charsets)

You can give Amazon Transcribe more information about how to process speech in your input file by creating a custom vocabulary\. A *custom vocabulary* is a list of specific words that you want Amazon Transcribe to recognize in your audio input\. These are generally domain\-specific words and phrases, words that Amazon Transcribe isn't recognizing, or proper nouns\.

Custom vocabularies work best when used to target specific words or phrases\. We recommend that you create separate small vocabularies tailored to specific audio recordings instead of creating a single vocabulary with many terms to use for all of your recordings\. You can have up to 100 vocabularies in your account\. The size limit for a custom vocabulary is 50 Kb\.

You specify the custom vocabulary in a text file\. You can specify either a list of words in the vocabulary, or a four\-column table that gives you more control over the input and output of the words in the custom vocabulary\.

For more information about creating a custom vocabulary, see [Create a Custom Vocabulary Using a List](#create-vocabulary-list) and [Create a Custom Vocabulary Using a Table](#create-vocabulary-table)\.

To create a custom vocabulary, use the [CreateVocabulary](API_CreateVocabulary.md) operation or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. After you submit the `CreateVocabulary` request, Amazon Transcribe processes the vocabulary\. To see the processing status of the vocabulary, use the console or the [GetVocabulary](API_GetVocabulary.md) operation\.

**Note**  
If you are uploading the custom vocabulary using the Amazon Transcribe console, you must use vocabulary list instead of a vocabulary table\. To use the console to create a custom vocabulary using a vocabulary table, the source file must be in an Amazon S3 bucket\.

To use the custom vocabulary, set the `VocabularyName` field of the `Settings` field when you call the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation or choose the vocabulary in the console when you create the transcription job\. 

## Create a Custom Vocabulary Using a List<a name="create-vocabulary-list"></a>

You can create a custom vocabulary using a list of words or phrases in a text file\. You can place each word on its own line, or you can put multiple words on a single line, separating the words or phrases from each other with a comma\. 

Each entry must contain:
+ Fewer than 256 characters, including hyphens
+ Only characters from the allowed character set

For valid character sets, see [Character Sets for Custom Vocabularies](#charsets)\.

If an entry is the list is a phrase, separate the words of the phrase with a hyphen\. For example, if the phrase is **Los Angeles**, you would enter it in the file as **Los\-Angeles**\.

Enter acronyms or other words whose letters should be pronounced individually as single letters separated by dots, such as **A\.B\.C\.** or **F\.B\.I\.**\. To enter the plural form of an acronym, such as "ABCs", separate the "s" from the acronym with a hyphen: **A\.B\.C\.\-s**\. You can use either upper or lower case letters to enter an acronym\. Acronyms are supported in the following languages:
+ Dutch
+ All English variants
+ All French variants
+ All German variants
+ Hindi
+ Indonesian
+ Italian
+ Malay
+ All Portuguese variants
+ All Spanish variants
+ Turkish

The following example shows an input file with the vocabulary words and phrases on separate lines:

```
Los-Angeles
F.B.I.
Etienne
```

The following example shows an input file with the vocabulary words and phrases on a single line, separated by commas:

```
Los-Angeles,F.B.I.,Etienne
```

## Create a Custom Vocabulary Using a Table<a name="create-vocabulary-table"></a>

You can create a custom vocabulary by creating a table in a text file\. Each row in the table is a word or phrase followed by the optional `IPA`, `SoundsLike`, and `DisplayAs` fields\. Each field must contain:
+ Fewer than 256 characters, including hyphens
+ Only characters from the allowed character set

For valid character sets, see [Character Sets for Custom Vocabularies](#charsets)

Place each word or phrase in your text file on a separate line\. Separate the fields with TAB characters\. Save the file with the extension `.txt` in an Amazon S3 bucket in the same region that you are calling the API\. 

The following examples are input files in text format\. The examples use spaces to align the columns\. Your input files should use TAB characters to separate the columns\. Include spaces only in the `IPA` and `DisplayAs` columns\. If you copy these examples, remove the extra spaces between columns and replace "\[TAB\]" with a TAB character\.

```
Phrase     [TAB]IPA       [TAB]SoundsLike[TAB]DisplayAs
Los-Angeles[TAB]          [TAB]          [TAB]Los Angeles
F.B.I.     [TAB]ɛ f b i aɪ[TAB]          [TAB]FBI
Etienne    [TAB]          [TAB]eh-tee-en [TAB]
```

Columns can be entered in any order\. The following are also valid structures for the custom vocabulary input file\.

```
Phrase     [TAB]SoundsLike[TAB]IPA       [TAB]DisplayAs
Los-Angeles[TAB]          [TAB]          [TAB]Los Angeles
F.B.I      [TAB]          [TAB]ɛ f b i aɪ[TAB]FBI
Etienne    [TAB]eh-tee-en [TAB]          [TAB]
```

```
DisplayAs  [TAB]SoundsLike[TAB]IPA       [TAB]Phrase
Los Angeles[TAB]          [TAB]          [TAB]Los-Angeles
FBI        [TAB]          [TAB]ɛ f b i aɪ[TAB]F.B.I.
           [TAB]eh-tee-en [TAB]          [TAB]Etienne
```
+ **Phrase** – The word or phrase that should be recognized\. 

  If the entry is a phrase, separate the words with a hyphen \(\-\)\. For example, you type **Los Angeles** as **Los\-Angeles**\.

  Enter acronyms or other words whose letters should be pronounced individually as single letters followed by dots, such **A\.B\.C\.** or **F\.B\.I\.**\. To enter the plural form of an acronym, such as "ABCs," separate the "s" from the acronym with a hyphen: "**A\.B\.C\.\-s**"\. You can use either upper\- or lower\-case letters to enter an acronym\. For a list of languages that support acronyms, see [Create a Custom Vocabulary Using a List](#create-vocabulary-list)\.

  The `Phrase` field is required\. You can use any of the allowed characters for the input language\. For the list of allowed characters, see the individual languages\. If you do not specify the `DisplayAs` field, Amazon Transcribe uses the contents of the `Phrase` field in the output file\.
+ **IPA** – To specify the pronunciation of your word or phrase, you can include characters in the [International Phonetic Alphabet \(IPA\)](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet) in this field\. The `IPA` field can't contain leading or trailing spaces, and you must use a single space to separate each phoneme in the input\. For example, in English you would enter the phrase **Los\-Angeles** as **l ɔ s æ n ʤ ə l ə s**\. You would enter the phrase **F\.B\.I\.** as **ɛ f b i aɪ**\.

  If you don't specify the contents of the `IPA` field, you must include a blank `IPA` field\. If you specify the `IPA` field, you can't specify the `SoundsLike` field\.

  For a list of allowed IPA characters for a specific language, see the table for individual languages\.
+ **SoundsLike** – You can break a word or phrase down into smaller pieces and provide a pronunciation for each piece using the standard orthography of the language to mimic the way that the word sounds\. For example, in English you can provide pronunciation hints for the phrase **Los\-Angeles** like this: **loss\-ann\-gel\-es**\. The hint for the word **Etienne** would look like this: **eh\-tee\-en**\. You separate each part of the hint with a hyphen \(\-\)\. 

  If you don't specify the `SoundsLike` field you must include a blank `SoundsLike` field\. If you specify the `SoundsLike` field you can't specify the `IPA` field\.

  You can use any of the allowed characters for the input language\. For the list of allowed characters, see the individual languages\.
+ **DisplayAs** – Defines the how the word or phrase looks when it's output\. For example, if the word or phrase is **Los\-Angeles**, you can specify the display form as "Los Angeles" so that the hyphen is not present in the output\.

  If you don't specify the `DisplayAs` field, Amazon Transcribe uses the `Phrase` field from the input file in the output\.

  You can use any UTF\-8 character in the `DisplayAs` field\.

## Character Sets for Custom Vocabularies<a name="charsets"></a>

 Amazon Transcribe limits the characters that you can use to create custom vocabularies\. You can use the following character sets for each language\.

**Topics**
+ [Arabic Character Set](#char-arabic)
+ [Chinese Character Set](#char-chinese)
+ [Dutch Character Set](#char-dutch)
+ [English Character Set](#char-english)
+ [Farsi Character Set](#char-farsi)
+ [French Character Set](#char-french)
+ [German Character Set](#char-german)
+ [Hebrew Character Set](#char-hebrew)
+ [Hindi Character Set](#char-hindi)
+ [Indonesian Character Set](#char-indonesian)
+ [Italian Character Set](#char-italian)
+ [Japanese Character Set](#char-japanese)
+ [Korean Character Set](#char-korean)
+ [Malay Character Set](#char-malay)
+ [Portuguese Character Set](#char-portuguese)
+ [Russian Character Set](#char-russian)
+ [Spanish Character Set](#char-spanish)
+ [Tamil Character Set](#char-tamil)
+ [Telugu Character Set](#char-telugu)
+ [Turkish Character Set](#char-turkish)

### Arabic Character Set<a name="char-arabic"></a>

For Arabic custom vocabularies, you can use the following Unicode characters in the `Phrase` and `SoundsLike` fields\. You can also use the hypen \(\-\) character to separate words\.


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| ء | 0621 | س | 0633 | 
| آ | 0622 | ش | 0634 | 
| أ | 0623 | ص | 0635 | 
| ؤ | 0624 | ض | 0636 | 
| إ | 0625 | ط | 0637 | 
| ئ | 0626 | ظ | 0638 | 
| ا | 0627 | ع | 0639 | 
| ب | 0628 | غ | 063A | 
| ة | 0629 | ف | 0641 | 
| ت | 062A | ق | 0642 | 
| ث | 062B | ك | 0643 | 
| ج | 062C | ل | 0644 | 
| ح | 062D | م | 0645 | 
| خ | 062E | ن | 0646 | 
| د | 062F | ه | 0647 | 
| ذ | 0630 | و | 0648 | 
| ر | 0631 | ى | 0649 | 
| ز | 0632 | ي | 064A | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of the vocabulary input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | tˤ | 0074 02E4 | 
| aː | 0061 02D0 | u | 0075 | 
| b | 0062 | uː | 0075 02D0 | 
| d | 0064 | v | 0076 | 
| dˤ | 0064 02E4 | w | 0077 | 
| f | 0066 | x | 0078 | 
| h | 0068 | z | 007A | 
| i | 0069 | zˤ | 007A 02E4 | 
| iː | 0069 02D0 | ð | 00F0 | 
| j | 006A | ðˤ | 00F0 02E4 | 
| k | 006B | ħ | 0127 | 
| l | 006C | ɣ | 0263 | 
| m | 006D | ɪ | 026A | 
| n | 006E | ɫ | 026B | 
| p | 0070 | ʃ | 0283 | 
| q | 0071 | ʒ | 0292 | 
| r | 0072 | ʔ | 0294 | 
| s | 0073 | ʕ | 0295 | 
| sˤ | 0073 02E4 | θ | 03B8 | 
| t | 0074 | χ | 03C7 | 

### Chinese Character Set<a name="char-chinese"></a>

 For Chinese custom vocabularies, the `Phrase` field can use any of the characters listed in the following file on GitHub\.
+ [chinese\-character\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/chinese-character-set.txt) 

The `SoundsLike` field can contain the pinyin syllables listed in the following file on GitHub\.
+ [pinyin\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/pinyin-set.txt) 

When you use pinyin syllables in the `SoundsLike` field, separate the syllables with a hyphen \(\-\)\.

Amazon Transcribe represents the four tones in Mandarin Chinese using numbers\. The following table shows how tone marks are mapped for the word "ma\."


| Tone | Tone Mark | Tone Number | 
| --- | --- | --- | 
| Tone 1 | mā | ma1 | 
| Tone 2 | má | ma2 | 
| Tone 3 | mǎ | ma3 | 
| Tone 4 | mà | ma4 | 

Chinese custom vocabularies don't use the `IPA` field, but you must still include the `IPA` header in the vocabulary table\. 

The following example is an input file in text format\. The example uses spaces to align the columns\. Your input files should use TAB characters to separate the columns\. Include spaces only in the `DisplayAs` column\.

```
Phrase     SoundsLike               IPA  DisplayAs
康健        kang1-jian4
谴责        qian3-ze2
国防大臣    guo2-fang2-da4-chen2
世界博览会  shi4-jie4-bo2-lan3-hui4       世博会
```

### Dutch Character Set<a name="char-dutch"></a>

For Dutch custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| à | 00E0 | î | 00EE | 
| á | 00E1 | ï | 00EF | 
| â | 00E2 | ñ | 00F1 | 
| ä | 00E4 | ò | 00F2 | 
| ç | 00E7 | ó | 00F3 | 
| è | 00E8 | ô | 00F4 | 
| é | 00E9 | ö | 00F6 | 
| ê | 00EA | ù | 00F9 | 
| ë | 00EB | ú | 00FA | 
| ì | 00EC | û | 00FB | 
| í | 00ED | ü | 00FC | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of the vocabulary input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a: | 0061 003A | z | 007A | 
| bː | 0062 02D0 | ø: | 00F8 003A | 
| b | 0062 | ŋ | 014B | 
| d | 0064 | œy | 0153 0079 | 
| eː | 0065 02D0 | œː | 0153 02D0 | 
| f | 0066 | ɑ | 0251 | 
| g | 0067 | ɔ | 0254 | 
| i | 0069 | ɔu | 0254 0075 | 
| j | 006A | ɔː | 0254 02D0 | 
| k | 006B | ə | 0259 | 
| l | 006C | ɛ | 025B | 
| m | 006D | ɛ: | 025B 003A | 
| n | 006E | ɛi | 025B 0069 | 
| oː | 006F 02D0 | ɦ | 0266 | 
| p | 0070 | ɪ | 026A | 
| s | 0073 | ɲ | 0272 | 
| t | 0074 | ɾ | 027E | 
| u | 0075 | ʃ | 0283 | 
| v | 0076 | ʏ | 028F | 
| w | 0077 | ʒ | 0292 | 
| y | 0079 | χ | 03C7 | 

### English Character Set<a name="char-english"></a>

For English custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can use the following International Phonetic Alphabet characters in the `IPA` field of the vocabulary input file:


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

### Farsi Character Set<a name="char-farsi"></a>

For Farsi custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields\.


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| ء | 0621 | ظ | 0638 | 
| آ | 0622 | ع | 0639 | 
| أ | 0623 | غ | 063A | 
| ؤ | 0624 | ف | 0641 | 
| ئ | 0626 | ق | 0642 | 
| ا | 0627 | ل | 0644 | 
| ب | 0628 | م | 0645 | 
| ت | 062A | ن | 0646 | 
| ث | 062B | ه | 0647 | 
| ج | 062C | و | 0648 | 
| ح | 062D | َ | 064E | 
| خ | 062E | ُ | 064F | 
| د | 062F | ِ | 0650 | 
| ذ | 0630 | ّ | 0651 | 
| ر | 0631 | پ | 067E | 
| ز | 0632 | چ | 0686 | 
| س | 0633 | ژ | 0698 | 
| ش | 0634 | ک | 06A9 | 
| ص | 0635 | گ | 06AF | 
| ض | 0636 | ی | 06CC | 
| ط | 0637 |   |   | 

You can use the following International Phonetic Alphabet in the `IPA` field of your vocabulary file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| b | 0062 | u | 0075 | 
| d | 0064 | v | 0076 | 
| f | 0066 | z | 007A | 
| g | 0067 | æ | 00E6 | 
| h | 0068 | ɒ | 0252 | 
| i | 0069 | ɛ | 025B | 
| j | 006A | ɾ | 027E | 
| k | 006B | ʁ | 0281 | 
| l | 006C | ʃ | 0283 | 
| m | 006D | ʒ | 0292 | 
| n | 006E | ʔ | 0294 | 
| o | 006F | ʔ | 0294 | 
| p | 0070 | ʤ | 02A4 | 
| s | 0073 | ʧ | 02A7 | 
| t | 0074 | χ | 03C7 | 

### French Character Set<a name="char-french"></a>

For French custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| À | 00C0 | à | 00E0 | 
| Â | 00C2 | â | 00E2 | 
| Ç | 00C7 | ç | 00E7 | 
| È | 00C8 | è | 00E8 | 
| É | 00C9 | é | 00E9 | 
| Ê | 00CA | ê | 00EA | 
| Ë | 00CB | ë | 00EB | 
| Î | 00CE | î | 00EE | 
| Ï | 00CF | ï | 00EF | 
| Ô | 00D4 | ô | 00F4 | 
| Ö | 00D6 | ö | 00F6 | 
| Ù | 00D9 | ù | 00F9 | 
| Û | 00DB | û | 00FB | 
| Ü | 00DC | ü | 00FC | 

You can use the following International Phonetic Alphabet in the `IPA` field of your vocabulary file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | z | 007A | 
| b | 0062 | ã | 00E3 | 
| d | 0064 | õ | 00F5 | 
| e | 0065 | ø | 00F8 | 
| f | 0066 | ŋ | 014B | 
| i | 0069 | œ | 0153 | 
| j | 006A | œ̃ | 0153 0303 | 
| k | 006B | ɐ | 0250 | 
| l | 006C | ɔ | 0254 | 
| m | 006D | ə | 0259 | 
| n | 006E | ɛ | 025B | 
| o | 006F | ɡ | 0261 | 
| p | 0070 | ɥ | 0265 | 
| s | 0073 | ɲ | 0272 | 
| t | 0074 | ʁ | 0281 | 
| u | 0075 | ʃ | 0283 | 
| v | 0076 | ʒ | 0292 | 
| w | 0077 | ẽ | 1EBD | 
| y | 0079 |   |   | 

### German Character Set<a name="char-german"></a>

For German custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| ä | 00E4 | Ä | 00C4 | 
| ö | 00F6 | Ö | 00D6 | 
| ü | 00FC | Ü | 00DC | 
| ß | 00DF |   |   | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of the vocabulary input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | ts | 0074 0073 | 
| aɪ | 0061 026A | uː | 0075 02D0 | 
| aʊ | 0061 028A | v | 0076 | 
| aː | 0061 02D0 | x | 0078 | 
| b | 0062 | z | 007A | 
| d | 0064 | yː | 0079 02D0 | 
| eː | 0065 02D0 | ã | 00E3 | 
| f | 0066 | ç | 00E7 | 
| g | 0067 | øː | 00F8 02D0 | 
| h | 0068 | ŋ | 014B | 
| iː | 0069 02D0 | œ | 0153 | 
| j | 006A | ɐ̯ | 0250 032F | 
| k | 006B | ɔ | 0254 | 
| l | 006C | ɔʏ | 0254 028F | 
| l̩ | 006C 0329 | ə | 0259 | 
| m | 006D | ɛ | 025B | 
| m̩ | 006D 0329 | ɛː | 025B 02D0 | 
| n | 006E | ɪ | 026A | 
| n̩ | 006E 0329 | ʁ | 0281 | 
| oː | 006F 02D0 | ʃ | 0283 | 
| p | 0070 | ʊ | 028A | 
| pf | 0070 0066 | ʏ | 028F | 
| s | 0073 | ʧ | 02A7 | 
| t | 0074 |   |   | 

### Hebrew Character Set<a name="char-hebrew"></a>

For Hebrew custom vocabularies, you can use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| \- | 002D | ם | 05DD | 
| א | 05D0 | מ | 05DE | 
| ב | 05D1 | ן | 05DF | 
| ג | 05D2 | נ | 05E0 | 
| ד | 05D3 | ס | 05E1 | 
| ה | 05D4 | ע | 05E2 | 
| ו | 05D5 | ף | 05E3 | 
| ז | 05D6 | פ | 05E4 | 
| ח | 05D7 | ץ | 05E5 | 
| ט | 05D8 | צ | 05E6 | 
| י | 05D9 | ק | 05E7 | 
| ך | 05DA | ר | 05E8 | 
| כ | 05DB | ש | 05E9 | 
| ל | 05DC | ת | 05EA | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of the vocabulary input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | p | 0070 | 
| b | 0062 | s | 0073 | 
| d | 0064 | t | 0074 | 
| e | 0065 | u | 0075 | 
| f | 0066 | v | 0076 | 
| g | 0067 | w | 0077 | 
| h | 0068 | z | 007A | 
| i | 0069 | ŋ | 014B | 
| j | 006A | ɣ | 0263 | 
| k | 006B | ʃ | 0283 | 
| l | 006C | ʒ | 0292 | 
| m | 006D | ʔ | 0294 | 
| n | 006E | χ | 03C7 | 
| o | 006F |   |   | 

### Hindi Character Set<a name="char-hindi"></a>

For Hindi custom vocabularies, you can use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| \- | 002D | थ | 0925 | 
| \. | 002E | द | 0926 | 
| ँ | 0901 | ध | 0927 | 
| ं | 0902 | न | 0928 | 
| ः | 0903 | प | 092A | 
| अ | 0905 | फ | 092B | 
| आ | 0906 | ब | 092C | 
| इ | 0907 | भ | 092D | 
| ई | 0908 | म | 092E | 
| उ | 0909 | य | 092F | 
| ऊ | 090A | र | 0930 | 
| ऋ | 090B | ल | 0932 | 
| ए | 090F | व | 0935 | 
| ऐ | 0910 | श | 0936 | 
| ओ | 0913 | ष | 0937 | 
| औ | 0914 | स | 0938 | 
| क | 0915 | ह | 0939 | 
| ख | 0916 | ा | 093E | 
| ग | 0917 | ि | 093F | 
| घ | 0918 | ी | 0940 | 
| ङ | 0919 | ु | 0941 | 
| च | 091A | ू | 0942 | 
| छ | 091B | ृ | 0943 | 
| ज | 091C | ॅ | 0945 | 
| झ | 091D | े | 0947 | 
| ञ | 091E | ै | 0948 | 
| ट | 091F | ॉ | 0949 | 
| ठ | 0920 | ो | 094B | 
| ड | 0921 | ौ | 094C | 
| ढ | 0922 | ् | 094D | 
| ण | 0923 | ज़ | 095B | 
| त | 0924 |   |   | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| aː | 0097 0720 | ŋ | 0331  | 
| b | 0098  | ɖ | 0598  | 
| bʱ | 0098 0689 | ɔː | 0596 0720 | 
| d | 0100  | ɖʱ | 0598 0689 | 
| dʱ | 0100 0689 | ə | 0601  | 
| eː | 0101 0720 | ɛː | 0603 0720 | 
| f | 0102  | ɡ | 0609  | 
| iː | 0105 0720 | ɡʱ | 0609 0689 | 
| j | 0106  | ɦ | 0614  | 
| k | 0107  | ɪ | 0618  | 
| kʰ | 0107 0688 | ɲ | 0626  | 
| l | 0108  | ɳ | 0627  | 
| m | 0109  | ɾ | 0638  | 
| n | 0110  | ʂ | 0642  | 
| oː | 0111 0720 | ʃ | 0643  | 
| p | 0112  | ʈ | 0648  | 
| pʰ | 0112 0688 | ʈʰ | 0648 0688 | 
| r | 0114  | ʊ | 0650  | 
| s | 0115  | ʋ | 0651  | 
| t | 0116  | ʤ | 0676  | 
| tʰ | 0116 0688 | ʤʱ | 0676 0689 | 
| uː | 0117 0720 | ʧ | 0679  | 
| z | 0122  | ʧʰ | 0679 0688 | 

### Indonesian Character Set<a name="char-indonesian"></a>

For Indonesian custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | r | 0072 | 
| ai | 0061 0069 | s | 0073 | 
| au | 0061 0075 | t | 0074 | 
| b | 0062 | tʃ | 0074 0283 | 
| d | 0064 | u | 0075 | 
| d | 0064 | v | 0076 | 
| e | 0065 | w | 0077 | 
| f | 0066 | x | 0078 | 
| h | 0068 | y | 0079 | 
| i | 0069 | ŋ | 014B | 
| j | 006A | ɔ | 0254 | 
| k | 006B | ə | 0259 | 
| l | 006C | ɛ | 025B | 
| m | 006D | ɡ | 0261 | 
| n | 006E | ɣ | 0263 | 
| o | 006F | ɪ | 026A | 
| oi̯ | 006F 0069 032F | ɲ | 0272 | 
| p | 0070 | ʃ | 0283 | 
| q | 0071 | ʊ | 028A | 

### Italian Character Set<a name="char-italian"></a>

For Italian custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| À | 00C0 | à | 00E0 | 
| Ä | 00C4 | ä | 00E4 | 
| Ç | 00C7 | ç | 00E7 | 
| È | 00C8 | è | 00E8 | 
| É | 00C9 | é | 00E9 | 
| Ê | 00CA | ê | 00EA | 
| Ë | 00CB | ë | 00EB | 
| Ì | 00CC | ì | 00EC | 
| Ò | 00D2 | ò | 00F2 | 
| Ù | 00D9 | ù | 00F9 | 
| Ü | 00DC | ü | 00FC | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | ss | 0073 0073 | 
| b | 0062 | t | 0074 | 
| bb | 0062 0062 | tt | 0074 0074 | 
| d | 0064 | u | 0075 | 
| dd | 0064 0064 | v | 0076 | 
| e | 0065 | vv | 0076 0076 | 
| f | 0066 | w | 0077 | 
| ff | 0066 0066 | z | 007A | 
| gg | 0067 0067 | ɔ | 0254 | 
| i | 0069 | ɛ | 025B | 
| j | 006A | ɡ | 0261 | 
| k | 006B | ɲ | 0272 | 
| kk | 006B 006B | ɲɲ | 0272 0272 | 
| l | 006C | ʃ | 0283 | 
| ll | 006C 006C | ʃʃ | 0283 0283 | 
| m | 006D | ʎ | 028E | 
| mm | 006D 006D | ʎʎ | 028E 028E | 
| n | 006E | ʣ | 02A3 | 
| nn | 006E 006E | ʣʣ | 02A3 02A3 | 
| o | 006F | ʤ | 02A4 | 
| p | 0070 | ʤʤ | 02A4 02A4 | 
| pp | 0070 0070 | ʦ | 02A6 | 
| r | 0072 | ʦʦ | 02A6 02A6 | 
| rr | 0072 0072 | ʧ | 02A7 | 
| s | 0073 | ʧʧ | 02A7 02A7 | 

### Japanese Character Set<a name="char-japanese"></a>

For Japanese custom vocabularies, the `Phrase` and `DisplayAs` fields can use any of the characters listed in the following file on GitHub\.
+ [ japanese\-character\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/japanese-character-set.txt) 

Amazon Transcribe supports Romaji characters in the `SoundsLike` field\. You can use the following lower\-case characters:
+ a \- k
+ m \- p
+ r \- w
+ y \- z

Represent long vowels by doubling the vowel:


| Vowel | Representation | 
| --- | --- | 
| ā | aa | 
| ē | ee | 
| ī | ii | 
| ō | oo | 
| ū | uu | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | p | 0070 | 
| aː | 0061 02D0 | s | 0073 | 
| b | 0062 | t | 0074 | 
| d | 0064 | ts | 0074 0073 | 
| dz | 0064 007A | tɕ | 0074 0255 | 
| dʑ | 0064 0291 | w | 0077 | 
| e | 0065 | z | 007A | 
| eː | 0065 02D0 | ç | 00E7 | 
| g | 0067 | ŋ | 014B | 
| h | 0068 | ɕ | 0255 | 
| i | 0069 | ɯ | 026F | 
| iː | 0069 02D0 | ɯː | 026F 02D0 | 
| j | 006A | ɴ | 0274 | 
| k | 006B | ɸ | 0278 | 
| m | 006D | ɾ | 027E | 
| n | 006E | ʑ | 0291 | 
| o | 006F | ʔ | 0294 | 
| oː | 006F 02D0 |   |   | 

### Korean Character Set<a name="char-korean"></a>

For Korean custom vocabularies, you can use any of the Hangul syllables in the `Phrase` and `SoundsLike` fields\. For more information, see [Hangul Syllables](https://en.wikipedia.org/wiki/Hangul_Syllables) on Wikipedia\.

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 00061 | s͈ | 0073 0348 | 
| e | 00065 | t | 0074 | 
| h | 00068 | tɕ | 0074 0255 | 
| i | 00069 | tɕʰ | 0074 0255 02B0 | 
| je | 006A 0065 | tʰ | 0074 02B0 | 
| jo | 006A 006F | t͈ | 0074 0348 | 
| ju | 006A 0075 | t͈ɕ | 0074 0348 0255 | 
| jɛ | 006A 025B | u | 0075 | 
| jʌ | 006A 028C | we | 0077 0065 | 
| ja | 006A 0061 | wi | 0077 0069 | 
| k | 006B | wɛ | 0077 025B | 
| kʰ | 006B 02B0 | wʌ | 0077 028C | 
| k͈ | 006B 0348 | wa | 0077 0061 | 
| l | 006C | ø | 00F8 | 
| m | 006D | ŋ | 0014B | 
| n | 006E | ɛ | 0025B | 
| o | 006F | ɯ | 026F | 
| p | 0070 | ɯi | 006F 0069 | 
| pʰ | 0070 02B0 | ɾ | 027E | 
| p͈ | 0070 0348 | ʌ | 028C | 
| s | 0073 |   |   | 

### Malay Character Set<a name="char-malay"></a>

For Malay custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| F | 0046 | r | 0072 | 
| a | 0061 | s | 0073 | 
| ai | 0061 0069 | t | 0074 | 
| au | 0061 0075 | tʃ | 0074 0283 | 
| b | 0062 | v | 0076 | 
| d | 0064 | w | 0077 | 
| dʒ | 0064 0292 | x | 0078 | 
| e | 0065 | y | 0079 | 
| h | 0068 | ŋ | 014B | 
| i | 0069 | ɔ | 0254 | 
| j | 006A | ə | 0259 | 
| k | 006B | ɛ | 025B | 
| l | 006C | ɡ | 0261 | 
| m | 006D | ɣ | 0263 | 
| n | 006E | ɪ | 026A | 
| o | 006F | ɲ | 0272 | 
| oi̯ | 006F 0069 32F | ʃ | 0283 | 
| p | 0070 | ʊ | 028A | 
| q | 0071 | ʊi | 028A 0069 | 

### Portuguese Character Set<a name="char-portuguese"></a>

For Portuguese custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| À | 00C0 | à | 00E0 | 
| Á | 00C1 | á | 00E1 | 
| Â | 00C2 | â | 00E2 | 
| Ã | 00C3 | ã | 00E3 | 
| Ä | 00C4 | ä | 00E4 | 
| Ç | 00C7 | ç | 00E7 | 
| È | 00C8 | è | 00E8 | 
| É | 00C9 | é | 00E9 | 
| Ê | 00CA | ê | 00EA | 
| Ë | 00CB | ë | 00EB | 
| Í | 00CD | í | 00ED | 
| Ñ | 00D1 | ñ | 00F1 | 
| Ó | 00D3 | ó | 00F3 | 
| Ô | 00D4 | ô | 00F4 | 
| Õ | 00D5 | õ | 00F5 | 
| Ö | 00D6 | ö | 00F6 | 
| Ú | 00DA | ú | 00FA | 
| Ü | 00DC | ü | 00FC | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | v | 0076 | 
| b | 0062 | w | 0077 | 
| d | 0064 | w̃ | 0077 0303 | 
| e | 0065 | z | 007A | 
| f | 0066 | õ | 00F5 | 
| g | 0067 | ĩ | 00129 | 
| i | 0069 | ũ | 00169 | 
| j | 006A | ɐ̃ | 0250 0303 | 
| k | 006B | ɔ | 0254 | 
| l | 006C | ɛ | 025B | 
| m | 006D | ɲ | 0272 | 
| n | 006E | ɾ | 027E | 
| o | 006F | ʁ | 0281 | 
| p | 0070 | ʃ | 0283 | 
| s | 0073 | ʎ | 028E | 
| t | 0074 | ʒ | 0292 | 
| tʃ | 0074 0283 | ʤ | 02A4 | 
| u | 0075 | ẽ | 1EBD | 

### Russian Character Set<a name="char-russian"></a>

For Russian custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| ' | 0027 | п | 043F | 
| \- | 002D | р | 0440 | 
| \. | 002E | с | 0441 | 
| а | 0430 | т | 0442 | 
| б | 0431 | у | 0443 | 
| в | 0432 | ф | 0444 | 
| г | 0433 | х | 0445 | 
| д | 0434 | ц | 0446 | 
| е | 0435 | ч | 0447 | 
| ж | 0436 | ш | 0448 | 
| з | 0437 | щ | 0449 | 
| и | 0438 | ъ | 044A | 
| й | 0439 | ы | 044B | 
| к | 043A | ь | 044C | 
| л | 043B | э | 044D | 
| м | 043C | ю | 044E | 
| н | 043D | я | 044F | 
| о | 043E | ё | 0451 | 

You can use the following International Phonetic Alphabet characters in the IPA field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| b | 0062 | t | 0074 | 
| bʲ | 0062 02B2 | tʃ | 0074 0283 | 
| d | 0064 | tʲ | 0074 02B2 | 
| dʲ | 0064 02B2 | u | 0075 | 
| f | 0066 | v | 0076 | 
| fʲ | 0066 02B2 | vʲ | 0076 02B2 | 
| g | 0067 | x | 0078 | 
| gʲ | 067 02B2 | xʲ | 0078 02B2 | 
| i | 0069 | z | 007A | 
| j | 006A | zʲ | 007A 02B2 | 
| k | 006B | æ | 00E6 | 
| kʲ | 006B 02B2 | ə | 0259 | 
| l | 006C | ɛ | 025B | 
| lʲ | 006C 02B2 | ɨ | 0268 | 
| m | 006D | ʃ | 0283 | 
| mʲ | 006D 02B2 | ʃʲ | 0283 02B2 | 
| n | 006E | ʊ | 028A | 
| nʲ | 006E 02B2 | ʌ | 028C | 
| p | 0070 | ʒ | 0292 | 
| pʲ | 0070 02B2 | ˈi | 02C8 0069 | 
| r | 0072 | ˈo | 02C8 006F | 
| rʲ | 0072 02B2 | ˈv | 02C8 0075 | 
| s | 0073 | ˈɛ | 02C8 025B | 
| sʲ | 0073 02B2 | ˈɨ | 02C8 0268 | 
| ts | 0074 0073 | ˈa | 02C8 0061 | 

### Spanish Character Set<a name="char-spanish"></a>

For Spanish custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| Á | 00C1 | á | 00E1 | 
| É | 00C9 | é | 00E9 | 
| Í | 00CD | ë | 00ED | 
| Ó | 00D3 | ó | 0XF3 | 
| Ú | 00DA | ú | 00FA | 
| Ñ | 00D1 | ñ | 0XF1 | 
| ü | 00FC |   |   | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | r | 0072 | 
| b | 0062 | s | 0073 | 
| d | 0064 | t | 0074 | 
| e | 0065 | u | 0075 | 
| f | 0066 | v | 0076 | 
| g | 0067 | w | 0077 | 
| h | 0068 | x | 0078 | 
| i | 0069 | z | 007A | 
| j | 006A | ŋ | 014B | 
| k | 006B | ɲ | 0272 | 
| l | 006C | ɾ | 027E | 
| m | 006D | ʃ | 0283 | 
| n | 006E | ʝ | 029D | 
| o | 006F | ʧ | 02A7 | 
| p | 0070 | θ | 03B8 | 

### Tamil Character Set<a name="char-tamil"></a>

For Tamil custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| அ | 0B85 | ர | 0BB0 | 
| ஆ | 0B86 | ல | 0BB2 | 
| இ | 0B87 | வ | 0BB5 | 
| ஈ | 0B88 | ழ | 0BB4 | 
| உ | 0B89 | ள | 0BB3 | 
| ஊ | 0B8A | ற | 0BB1 | 
| எ | 0B8E | ன | 0BA9 | 
| ஏ | 0B8F | ஜ | 0B9C | 
| ஐ | 0B90 | ஶ | 0BB6 | 
| ஒ | 0B92 | ஷ | 0BB7 | 
| ஓ | 0B93 | ஸ | 0BB8 | 
| ஔ | 0B94 | ஹ | 0BB9 | 
| ஃ | 0B83 | ் | 0BCD | 
| க | 0B95 | ா | 0BBE | 
| ங | 0B99 | ி | 0BBF | 
| ச | 0B9A | ீ | 0BC0 | 
| ஞ | 0B9E | ு | 0BC1 | 
| ட | 0B9F | ூ | 0BC2 | 
| ண | 0BA3 | ெ | 0BC6 | 
| த | 0BA4 | ே | 0BC7 | 
| ந | 0BA8 | ை | 0BC8 | 
| ப | 0BAA | ொ | 0BCA | 
| ம | 0BAE | ோ | 0BCB | 
| ய | 0BAF | ௌ | 0BCC | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | v | 0076 | 
| aː | 0061 02D0 | w | 0077 | 
| b | 0062 | z | 007A | 
| d | 0064 | æ | 00E6 | 
| dʒ | 0064 0292 | ð | 00F0 | 
| e | 0065 | ŋ | 014B | 
| f | 0066 | ɑ | 0251 | 
| g | 0067 | ɔ | 0254 | 
| h | 0068 | ə | 0259 | 
| i | 0069 | ɛ | 025B | 
| iː | 0069 02D0 | ɡ | 0261 | 
| j | 006A | ɪ | 026A | 
| k | 006B | ɭ | 026D | 
| l | 006C | ɲ | 0272 | 
| m | 006D | ɳ | 0273 | 
| n | 006E | ɹ | 0279 | 
| n̪ | 006E 032A | ɹ | 0279 | 
| o | 006F | ɹ̩ | 0279 0329 | 
| oː | 006F 02D0 | ɾ | 027E | 
| p | 0070 | ʂ | 0282 | 
| r | 0072 | ʃ | 0283 | 
| s | 0073 | ʈ | 0288 | 
| t | 0074 | ʊ | 028A | 
| t̪ | 0074 032A | ʋ | 028B | 
| tʃ | 0074 0283 | ʌ | 028C | 
| u | 0075 | ʒ | 0292 | 
| uː | 0075 02D0 | θ | 03B8 | 

### Telugu Character Set<a name="char-telugu"></a>

For Telugu custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| \- | 002D | త | 0C24 | 
| ఁ | 0C01 | థ | 0C25 | 
| ం | 0C02 | ద | 0C26 | 
| ః | 0C03 | ధ | 0C27 | 
| అ | 0C05 | న | 0C28 | 
| ఆ | 0C06 | ప | 0C2A | 
| ఇ | 0C07 | ఫ | 0C2B | 
| ఈ | 0C08 | బ | 0C2C | 
| ఉ | 0C09 | భ | 0C2D | 
| ఊ | 0C0A | మ | 0C2E | 
| ఋ | 0C0B | య | 0C2F | 
| ఌ | 0C0C | ర | 0C30 | 
| ఎ | 0C0E | ఱ | 0C31 | 
| ఏ | 0C0F | ల | 0C32 | 
| ఐ | 0C10 | ళ | 0C33 | 
| ఒ | 0C12 | వ | 0C35 | 
| ఓ | 0C13 | శ | 0C36 | 
| ఔ | 0C14 | ష | 0C37 | 
| క | 0C15 | స | 0C38 | 
| ఖ | 0C16 | హ | 0C39 | 
| గ | 0C17 | ా | 0C3E | 
| ఘ | 0C18 | ి | 0C3F | 
| ఙ | 0C19 | ీ | 0C40 | 
| చ | 0C1A | ు | 0C41 | 
| ఛ | 0C1B | ూ | 0C42 | 
| జ | 0C1C | ృ | 0C43 | 
| ఝ | 0C1D | ౄ | 0C44 | 
| ఞ | 0C1E | ే | 0C47 | 
| ట | 0C1F | ై | 0C48 | 
| ఠ | 0C20 | ొ | 0C4A | 
| డ | 0C21 | ో | 0C4B | 
| ఢ | 0C22 | ౌ | 0C4C | 
| ణ | 0C23 | ్ | 0C4D | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| d̪ | 0064 032A | ð | 00F0 | 
| d̪̤ | 0064 032A 0324 | ŋ | 014B | 
| dʒ | 0064 0292 | ɑ | 0251 | 
| dʒ̤ | 0064 0292 0324 | ɔ | 0254 | 
| e | 0065 | ɖ | 0256 | 
| eː | 0065 02D0 | ɖ̤ | 0256 0324 | 
| f | 0066 | ə | 0259 | 
| h | 0068 | ɛ | 025B | 
| i | 0069 | ɡ | 0261 | 
| iʐ | 0069 0290 | ɡ̤ | 0261 0324 | 
| j | 006A | ɪ | 026A | 
| k | 006B | ɭ | 026D | 
| kʰ | 006B 02B0 | ɲ | 0272 | 
| l | 006C | ɳ | 0273 | 
| m | 006D | ɹ | 0279 | 
| n | 006E | ɹ̩ | 0279 0329 | 
| o | 006F | ɽ | 027D | 
| oː | 006F 02D0 | ʂ | 0282 | 
| p | 0070 | ʃ | 0283 | 
| pʰ | 0070 02B0 | ʈ | 0288 | 
| r | 0072 | ʈʰ | 0288 02B0 | 
| s | 0073 | ʊ | 028A | 
| t | 0074 | ʋ | 028B | 
| t̪ | 0074 032A | ʌ | 028C | 
| t̪ʰ | 0074 032A 02B0 | ʒ | 0292 | 
| t | 0074 | θ | 03B8 | 
| tʃʰ | 0074 0283 02B0 |   |   | 

### Turkish Character Set<a name="char-turkish"></a>

For Turkish custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| Ç | 00C7 | ö | 00F6 | 
| Ö | 00D6 | û | 00FB | 
| Ü | 00DC | ü | 00FC | 
| â | 00E2 | Ğ | 011E | 
| ä | 00E4 | ğ | 011F | 
| ç | 00E7 | İ | 0130 | 
| è | 00E8 | ı | 0131 | 
| é | 00E9 | Ş | 015E | 
| ê | 00EA | ş | 015F | 
| í | 00ED | š | 0161 | 
| î | 00EE | ž | 017E | 
| ó | 00F3 |   |   | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | u | 0075 | 
| aː | 0061 02D0 | uː | 0075 02D0 | 
| b | 0062 | v | 0076 | 
| c | 0063 | w | 0077 | 
| d | 0064 | y | 0079 | 
| e | 0065 | yː | 0079 02D0 | 
| eː | 0065 02D0 | z | 007A | 
| f | 0066 | ø | 00F8 | 
| g | 0067 | øː | 00F8 02D0 | 
| h | 0068 | ŋ | 014B | 
| i | 0069 | ɟ | 025F | 
| iː | 0069 02D0 | ɣ | 0263 | 
| j | 006A | ɫ | 026B | 
| k | 006B | ɯ | 026F | 
| l | 006C | ɯː | 026F 02D0 | 
| m | 006D | ɾ | 027E | 
| n | 006E | ʃ | 0283 | 
| o | 006F | ʒ | 0292 | 
| oː | 006F 02D0 | ʔ | 0294 | 
| p | 0070 | ʤ | 02A4 | 
| s | 0073 | ʧ | 02A7 | 
| t | 0074 |   |   | 
