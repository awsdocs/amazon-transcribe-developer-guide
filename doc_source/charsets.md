# Character sets for custom vocabularies<a name="charsets"></a>

 Amazon Transcribe limits the characters that you can use to create custom vocabularies\. You can use the following character sets for each language\.

**Important**  
Be sure to check that your custom vocabulary file uses only the supported Unicode code points and code point sequences listed within the following character sets\.

Many Unicode characters can appear identical in popular fonts, even if they use different code points\. **Only the code points listed in this guide are supported**\. For example, the French word **déjà** can be rendered using *precomposed* characters \(where one Unicode value represents an accented character\) or *decomposed* characters \(where two Unicode values represent an accented character, one value for the base character and another for the accent\)\.
+ **Precomposed version**: 0064 **00E9** 006A **00E0** \(renders as **déjà**\) 
+ **Decomposed version**: 0064 **0065 0301** 006A **0061 0300** \(renders as **déjà**\)

**Topics**
+ [Afrikaans character set](#char-afrikaans)
+ [Arabic character set](#char-arabic)
+ [Chinese, Mandarin \(Mainland China\), Simplified character set](#char-chinese-man-cn)
+ [Chinese, Mandarin \(Taiwan\), Traditional character set](#char-chinese-man-tw)
+ [Danish character set](#char-danish)
+ [Dutch character set](#char-dutch)
+ [English character set](#char-english)
+ [Farsi character set](#char-farsi)
+ [French character set](#char-french)
+ [German character set](#char-german)
+ [Hebrew character set](#char-hebrew)
+ [Hindi character set](#char-hindi)
+ [Indonesian character set](#char-indonesian)
+ [Italian character set](#char-italian)
+ [Japanese character set](#char-japanese)
+ [Korean character set](#char-korean)
+ [Malay character set](#char-malay)
+ [Portuguese character set](#char-portuguese)
+ [Russian character set](#char-russian)
+ [Spanish character set](#char-spanish)
+ [Tamil character set](#char-tamil)
+ [Telugu character set](#char-telugu)
+ [Thai character set](#char-thai)
+ [Turkish character set](#char-turkish)

## Afrikaans character set<a name="char-afrikaans"></a>

For Afrikaans custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| á | 00E1 | ï | 00EF | 
| è | 00E8 | ó | 00F3 | 
| é | 00E9 | ô | 00F4 | 
| ê | 00EA | ö | 00F6 | 
| ë | 00EB | ú | 00FA | 
| í | 00ED | û | 00FB | 
| î | 00EE | ü | 00FC | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of the vocabulary input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | z | 007A | 
| b | 0062 | æ | 00E6 | 
| c | 0063 | ð | 00F0 | 
| d | 0064 | ø | 00F8 | 
| e | 0065 | ŋ | 014B | 
| ẽ | 0065 0303 | œ | 0153 | 
| f | 0066 | ɐ | 0250 | 
| g | 0067 | ɑ | 0251 | 
| h | 0068 | ɑ̃ | 0251 0303 | 
| i | 0069 | ɒ | 0252 | 
| j | 006A | ɔ | 0254 | 
| k | 006B | ɔ̃ | 0254 0303 | 
| l | 006C | ə | 0259 | 
| m | 006D | ɛ | 025B | 
| n | 006E | ɛ̃ | 025B 0303 | 
| o | 006F | ɜ | 025C | 
| õ | 006F 0303 | ɪ | 026A | 
| p | 0070 | ɬ | 026C | 
| r | 0072 | ɹ | 0279 | 
| s | 0073 | ʁ | 0281 | 
| t | 0074 | ʃ | 0283 | 
| u | 0075 | ʊ | 028A | 
| v | 0076 | ʌ | 028C | 
| w | 0077 | ʒ | 0292 | 
| x | 0078 | θ | 03B8 | 
| y | 0079 | 

## Arabic character set<a name="char-arabic"></a>

For Arabic custom vocabularies, you can use the following Unicode characters in the `Phrase` and `SoundsLike` fields\. You can also use the hyphen \(\-\) character to separate words\.


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

## Chinese, Mandarin \(Mainland China\), Simplified character set<a name="char-chinese-man-cn"></a>

For Chinese \(Simplified\) custom vocabularies, the `Phrase` field can use any of the characters listed in the following file on GitHub\.
+ [zh\-cn\-character\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/zh-cn-character-set.txt) 

The `SoundsLike` field can contain the pinyin syllables listed in the following file on GitHub\.
+ [pinyin\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/pinyin-set.txt) 

When you use pinyin syllables in the `SoundsLike` field, separate the syllables with a hyphen \(\-\)\.

Amazon Transcribe represents the four tones in Chinese \(Simplified\) using numbers\. The following table shows how tone marks are mapped for the word 'ma'\.


| Tone | Tone mark | Tone number | 
| --- | --- | --- | 
| Tone 1 | mā | ma1 | 
| Tone 2 | má | ma2 | 
| Tone 3 | mǎ | ma3 | 
| Tone 4 | mà | ma4 | 

**Note**  
For the 5th \(neutral\) tone, you can use Tone 1, with the exception of 'er', which must be mapped to Tone 2\. For example, 打转儿 would be represented as 'da3\-zhuan4\-er2'\.

Chinese \(Simplified\) custom vocabularies don't use the `IPA` field, but you must still include the `IPA` header in the vocabulary table\. 

The following example is an input file in text format\. The example uses spaces to align the columns\. Your input files should use TAB characters to separate the columns\. Include spaces only in the `DisplayAs` column\.

```
Phrase       SoundsLike               IPA     DisplayAs
康健          kang1-jian4 
谴责          qian3-ze2 
国防大臣      guo2-fang2-da4-chen2 
世界博览会    shi4-jie4-bo2-lan3-hui4          世博会
```

## Chinese, Mandarin \(Taiwan\), Traditional character set<a name="char-chinese-man-tw"></a>

 For Chinese \(Traditional\) custom vocabularies, the `Phrase` field can use any of the characters listed in the following file on GitHub\.
+ [zh\-tw\-character\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/zh-tw-character-set.txt) 

The `SoundsLike` field can contain the zhuyin syllables listed in the following file on GitHub\.
+ [zhuyin\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/zhuyin-set.txt) 

When you use zhuyin syllables in the `SoundsLike` field, separate the syllables with a hyphen \(\-\)\.

Amazon Transcribe represents the four tones in Chinese \(Traditional\) using numbers\. The following table shows how tone marks are mapped for the word ㄇㄚ\.


| Tone | Tone mark | 
| --- | --- | 
| Tone 1 | ㄇㄚ | 
| Tone 2 | ㄇㄚˊ | 
| Tone 3 | ㄇㄚˇ | 
| Tone 4 | ㄇㄚˋ | 

Chinese \(Traditional\) custom vocabularies don't use the `IPA` field, but you must still include the `IPA` header in the vocabulary table\.

The following example is an input file in text format\. The example uses spaces to align the columns\. Your input files should use TAB characters to separate the columns\. Include spaces only in the `DisplayAs` column\.

```
Phrase        SoundsLike                     IPA        DisplayAs
健康          ㄐㄧㄢˋ-ㄎㄤ 
譴責          ㄑㄧㄢˇ-ㄗㄜˊ 
國防部長      ㄍㄨㄛˊ-ㄈㄤˊ-ㄅㄨˋ-ㄓㄤˇ 
世界博覽會     ㄕˋ-ㄐㄧㄝˋ-ㄅㄛˊ-ㄌㄢˇ-ㄏㄨㄟˋ             世博會
```

## Danish character set<a name="char-danish"></a>

For Danish custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ a \- z
+ A \- Z
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| Å | 00C5 | æ | 00E6 | 
| Æ | 00C6 | é | 00E9 | 
| Ø | 00D8 | ø | 00F8 | 
| å | 00E5 | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of the vocabulary input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | æ | 00E6 | 
| b | 0062 | ð | 00F0 | 
| d | 0064 | ø | 00F8 | 
| e | 0065 | ŋ | 014B | 
| f | 0066 | œ | 0153 | 
| h | 0068 | ɐ | 0250 | 
| i | 0069 | ɑ | 0251 | 
| j | 006A | ɒ | 0252 | 
| kʰ | 006B 02B0 | ɔ | 0254 | 
| l | 006C | ɕ | 0255 | 
| m | 006D | ə | 0259 | 
| n | 006E | ɛ | 025B | 
| o | 006F | ɡ | 0261 | 
| pʰ | 0070 02B0 | ɪ | 026A | 
| s | 0073 | ʁ | 0281 | 
| tˢ | 0074 02E2 | ʊ | 028A | 
| u | 0075 | ʋ | 028B | 
| w | 0077 | ʌ | 028C | 
| y | 0079 | 

## Dutch character set<a name="char-dutch"></a>

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
| a: | 0061 003A | ø: | 00F8 003A | 
| bː | 0062 02D0 | ŋ | 014B | 
| b | 0062 | œy | 0153 0079 | 
| d | 0064 | œː | 0153 02D0 | 
| eː | 0065 02D0 | ɑ | 0251 | 
| f | 0066 | ɔ | 0254 | 
| g | 0067 | ɔu | 0254 0075 | 
| i | 0069 | ɔː | 0254 02D0 | 
| j | 006A | ə | 0259 | 
| k | 006B | ɛ | 025B | 
| l | 006C | ɛ: | 025B 003A | 
| m | 006D | ɛi | 025B 0069 | 
| n | 006E | ɦ | 0266 | 
| oː | 006F 02D0 | ɪ | 026A | 
| p | 0070 | ɲ | 0272 | 
| s | 0073 | ɾ | 027E | 
| t | 0074 | ʃ | 0283 | 
| u | 0075 | ʏ | 028F | 
| v | 0076 | ʒ | 0292 | 
| w | 0077 | χ | 03C7 | 
| y | 0079 | ɣ | 0263 | 
| z | 007A |  |  | 

## English character set<a name="char-english"></a>

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

## Farsi character set<a name="char-farsi"></a>

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

## French character set<a name="char-french"></a>

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

## German character set<a name="char-german"></a>

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

## Hebrew character set<a name="char-hebrew"></a>

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

## Hindi character set<a name="char-hindi"></a>

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
| ऑ | 0911 | ष | 0937 | 
| ओ | 0913 | स | 0938 | 
| औ | 0914 | ह | 0939 | 
| क | 0915 | ा | 093E | 
| ख | 0916 | ि | 093F | 
| ग | 0917 | ी | 0940 | 
| घ | 0918 | ु | 0941 | 
| ङ | 0919 | ू | 0942 | 
| च | 091A | ृ | 0943 | 
| छ | 091B | ॅ | 0945 | 
| ज | 091C | े | 0947 | 
| झ | 091D | ै | 0948 | 
| ञ | 091E | ॉ | 0949 | 
| ट | 091F | ो | 094B | 
| ठ | 0920 | ौ | 094C | 
| ड | 0921 | ् | 094D | 
| ढ | 0922 | ज़ | 095B | 
| ण | 0923 | ड़ | 095C | 
| त | 0924 | ढ़ | 095D | 

Amazon Transcribe maps the following characters:


| Character | Mapped to | 
| --- | --- | 
| ऩ \(0929\) | न \(0928\) | 
| ऱ \(0931\) | र \(0930\) | 
| क़ \(0958\) | क \(0915\) | 
| ख़ \(0959\) | ख \(0916\) | 
| ग़ \(095A\) | ग \(0917\) | 
| फ़ \(095E\) | फ \(092B\) | 
| य़ \(095F\) | य \(092F\) | 

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

## Indonesian character set<a name="char-indonesian"></a>

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
| d​ʒ | 0064 0292 | v | 0076 | 
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

## Italian character set<a name="char-italian"></a>

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

## Japanese character set<a name="char-japanese"></a>

For Japanese custom vocabularies, the `Phrase` and `SoundsLike` fields can use any of the characters listed in the following file on GitHub\.
+ [ ja\-jp\-character\-set\.txt](https://github.com/awsdocs/amazon-transcribe-developer-guide/blob/master/doc_source/ja-jp-character-set.txt) 

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

## Korean character set<a name="char-korean"></a>

For Korean custom vocabularies, you can use any of the Hangul syllables in the `Phrase` and `SoundsLike` fields\. For more information, see [Hangul Syllables](https://en.wikipedia.org/wiki/Hangul_Syllables) on Wikipedia\.

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | s | 0073 | 
| e | 0065 | s͈ | 0073 0348 | 
| h | 0068 | t | 0074 | 
| i | 0069 | tɕ | 0074 0255 | 
| je | 006A 0065 | tɕʰ | 0074 0255 02B0 | 
| jo | 006A 006F | tʰ | 0074 02B0 | 
| ju | 006A 0075 | t͈ | 0074 0348 | 
| jɛ | 006A 025B | t̚ | 0074 031A | 
| jʌ | 006A 028C | t͈ɕ | 0074 0348 0255 | 
| ja | 006A 0061 | u | 0075 | 
| k | 006B | we | 0077 0065 | 
| kʰ | 006B 02B0 | wi | 0077 0069 | 
| k͈ | 006B 0348 | wɛ | 0077 025B | 
| k̚ | 006B 031A | wʌ | 0077 028C | 
| l | 006C | wa | 0077 0061 | 
| m | 006D | ø | 00F8 | 
| n | 006E | ŋ | 0014B | 
| o | 006F | ɛ | 0025B | 
| p | 0070 | ɯ | 026F | 
| pʰ | 0070 02B0 | ɯi | 006F 0069 | 
| p͈ | 0070 0348 | ɾ | 027E | 
| p̚ | 0070 031A | ʌ | 028C | 

## Malay character set<a name="char-malay"></a>

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

## Portuguese character set<a name="char-portuguese"></a>

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
| a | 0061 | s | 0073 | 
| b | 0062 | t | 0074 | 
| d | 0064 | tʃ | 0074 0283 | 
| e | 0065 | u | 0075 | 
| ẽ | 1EBD | ũ | 00169 | 
| f | 0066 | v | 0076 | 
| g | 0067 | w | 0077 | 
| i | 0069 | w̃ | 0077 0303 | 
| ĩ | 00129 | z | 007A | 
| j | 006A | ɐ̃ | 0250 0303 | 
| j̃ | 006A 0303 | ɔ | 0254 | 
| k | 006B | ɛ | 025B | 
| l | 006C | ɲ | 0272 | 
| m | 006D | ɾ | 027E | 
| n | 006E | ʁ | 0281 | 
| o | 006F | ʃ | 0283 | 
| õ | 00F5 | ʎ | 028E | 
| p | 0070 | ʒ | 0292 | 
| r | 0072 | ʤ | 02A4 | 

## Russian character set<a name="char-russian"></a>

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

## Spanish character set<a name="char-spanish"></a>

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

## Tamil character set<a name="char-tamil"></a>

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

## Telugu character set<a name="char-telugu"></a>

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

## Thai character set<a name="char-thai"></a>

For Thai custom vocabularies, you can use the following characters in the `Phrase` and `SoundsLike` fields:
+ \- \(hyphen\)
+ \. \(period\)

You can also use the following Unicode characters in the `Phrase` and `SoundsLike` fields:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| ก | 0E01 | ล | 0E25 | 
| ข | 0E02 | ฦ | 0E26 | 
| ฃ | 0E03 | ว | 0E27 | 
| ค | 0E04 | ศ | 0E28 | 
| ฅ | 0E05 | ษ | 0E29 | 
| ฆ | 0E06 | ส | 0E2A | 
| ง | 0E07 | ห | 0E2B | 
| จ | 0E08 | ฬ | 0E2C | 
| ฉ | 0E09 | อ | 0E2D | 
| ช | 0E0A | ฮ | 0E2E | 
| ซ | 0E0B | ฯ | 0E2F | 
| ฌ | 0E0C | ะ | 0E30 | 
| ญ | 0E0D | ั | 0E31 | 
| ฎ | 0E0E | า | 0E32 | 
| ฏ | 0E0F | ิ | 0E34 | 
| ฐ | 0E10 | ี | 0E35 | 
| ฑ | 0E11 | ึ | 0E36 | 
| ฒ | 0E12 | ื | 0E37 | 
| ณ | 0E13 | ุ | 0E38 | 
| ด | 0E14 | ู | 0E39 | 
| ต | 0E15 | ฺ | 0E3A | 
| ถ | 0E16 | เ | 0E40 | 
| ท | 0E17 | แ | 0E41 | 
| ธ | 0E18 | โ | 0E42 | 
| น | 0E19 | ใ | 0E43 | 
| บ | 0E1A | ไ | 0E44 | 
| ป | 0E1B | ๅ | 0E45 | 
| ผ | 0E1C | ๆ | 0E46 | 
| ฝ | 0E1D | ็ | 0E47 | 
| พ | 0E1E | ่ | 0E48 | 
| ฟ | 0E1F | ้ | 0E49 | 
| ภ | 0E20 | ๊ | 0E4A | 
| ม | 0E21 | ๋ | 0E4B | 
| ย | 0E22 | ์ | 0E4C | 
| ร | 0E23 | ํ | 0E4D | 
| ฤ | 0E24 | 

You can use the following International Phonetic Alphabet characters in the `IPA` field of your input file:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| a | 0061 | pʰ | 0070 02B0 | 
| aː | 0061 02D0 | r | 0072 | 
| b | 0062 | s | 0073 | 
| d | 0064 | t | 0074 | 
| e | 0065 | tʰ | 0074 02B0 | 
| eː | 0065 02D0 | tˉɕ | 0074 0361 0255 | 
| f | 0066 | tˉɕʰ | 0074 0361 0255 02B0 | 
| h | 0068 | u | 0075 | 
| i | 0069 | uː | 0075 02D0 | 
| iː | 0069 02D0 | uːa | 0075 02D0 0061 | 
| iːa | 0069 02D0 0061 | w | 0077 | 
| j | 006A | ŋ | 014B | 
| k | 006B | ɔ | 0254 | 
| kw | 006B 0077 | ɔː | 0254 02D0 | 
| kʰ | 006B 02B0 | ɛ | 025B | 
| kʰw | 006B 02B0 0077 | ɛː | 025B 02D0 | 
| l | 006C | ɤ | 0264 | 
| m | 006D | ɤː | 0264 02D0 | 
| n | 006E | ɯ | 026F | 
| o | 006F | ɯː | 026F 02D0 | 
| oː | 006F 02D0 | ɯːa | 026F 02D0 0061 | 
| p | 0070 | ʔ | 0294 | 

## Turkish character set<a name="char-turkish"></a>

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