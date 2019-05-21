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

If an entry is the list is a phrase, separate the words of the phrase with a hypen\. For example, if the phrase is **Los Angeles**, you would enter it in the file as **Los\-Angeles**\.

Enter acronyms or other words whose letters should be pronounced individually as single letters separated by dots, such as **A\.B\.C\.** or **F\.B\.I\.**\. To enter the plural form of an acronym, such as "ABCs", separate the "s" from the acronym with a hyphen: **A\.B\.C\.\-s**\. You can use either upper or lower case letters to enter an acronym\. Acronyms are only supported in US English \(en\-US\)\.

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

Place each word or phrase in your text file on a separate line\. Save the file in an Amazon S3 bucket in the same region that you are calling the API with the extension \.txt\. 

The following is an example input file in text format\. 

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

  Enter acronyms or other words whose letters should be pronounced individually as single letters followed by dots, such **A\.B\.C\.** or **F\.B\.I\.**\. To enter the plural form of an acronym, such as "ABCs," separate the "s" from the acronym with a hyphen: "**A\.B\.C\.\-s**"\. You can use either upper\- or lower\-case letters to enter an acronym\. Acronyms are supported only in US English \(en\-US\)\.

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
+ [English Character Set](#char-english)
+ [French Character Set](#char-french)
+ [German Character Set](#char-german)
+ [Hindi Character Set](#char-hindi)
+ [Italian Character Set](#char-italian)
+ [Korean Character Set](#char-korean)
+ [Portuguese Character Set](#char-portuguese)
+ [Spanish Character Set](#char-spanish)

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
| त | 0924 | ‘ | 2018 | 

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
| mm | 006D 006D | ʎʎ | 028e 028e | 
| n | 006E | ʣ | 02A3 | 
| nn | 006E 06E | ʣʣ | 02A3 02A3 | 
| o | 006F | ʤ | 02A4 | 
| p | 0070 | ʤʤ | 02A4 02A4 | 
| pp | 0070 0070 | ʦ | 02A6 | 
| r | 0072 | ʦʦ | 02A6 02A6 | 
| rr | 0072 0072 | ʧ | 02A7 | 
| s | 0073 | ʧʧ | 02A7 02A7 | 

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