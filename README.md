# Ukrainian Etymological Dictionary

This is a database containing the articles of the Ukrainian Etymological Dictionary based on the OCRed version used on some websites. This revision includes corrections of distortions caused by OCR and other minor enhancements. Additionally, it contains a list of links pointing to articles rather than to words, an amplified list of languages and a list of abbreviations, for the one found in the paper version is far from being exhaustive (and is completely missing in the web version).

## Sources

Initial data was taken from the [LinguisticAndInformationSystems
 database](https://github.com/LinguisticAndInformationSystems/mphdict). Additionally were used the [scans](http://litopys.org.ua/djvu/etymolog_slovnyk.htm) of the dictionary's paper version.

## Contents and structure

The repository contains four databases:
1. Articles.
2. Links between articles.
3. List of language abbreviations.
4. List of other abbreviations used in the dictionary.

### Articles

Structure:
* `id`: id of the article assigned alphabetically;
* `word`: headword of the article;
* `homonym`: number of the homonym (0 if the headword has no homonyms);
* `heading`: the first part of the article – the headword with (optionally) its definition or other clarification of meaning;
* `derivatives`: variants of the headword, derivatives from it or from its root;
* `slavic_counterparts`: etymological counterparts of the headword in other Slavic languages;
* `etymology`: main text explaining etymology with separate phrases delimited by `#` surrounded by spaces;
* `volume`: volume of the dictionary containing the article;
* `pages`: page(s) in the paper dictionary containing the article.


Notes: 
* Articles are sorted alphabetically: *ґ* goes between *г* and *д*, *ь* – between *щ* and *ю*, so the order is different from the one in the paper version.
* Articles consisting only of the link (and a list of derivatives) are not present here. Words from such articles are contained in the 'derivatives' sections of the ones to which they are linking (e.g. *свірк* is contained in the article for *сверені́ти* along with its own derivative *свірко*).
* In cases when the article for one of the homonyms contained only a link and was thus removed, the numbers of other homonyms were retained for consistency (see *мі́сячник*).
* Stress was additionally marked for some headwords if it was mentioned in links pointing to the respective articles.

### Links

Structure:
* `id_linking`: id of the article (from the [Articles](#articles) table) which contains the link;
* `type`: type of the link: 0 for `див.` ('see'), 1 for `пор.` ('compare');
* `number`: number of the link among the links of given type from the given article;
* `id_linked`: id of the article (from the [Articles](#articles) table) to which the link points.

Notes:
* Links to removed articles (those containing only other links, see [Articles](#articles) section) are redirected to the relevant articles (e.g. *мо́ршки́* is now pointing directly to *сморг*, not to *сморж*, which contained no etymology). 
* Some links in the dictionary point to words with no corresponding articles. If they turned out to be derivatives of the words contained in the dictionary, the links were redirected to related articles (e.g. *барабо́ля¹* in the paper dictionary points to *мандибу́рка*; in the absence of such article the link was redirected to *мандебу́рка* article, where *мандибу́рка* is listed as a spelling variant).
* Links pointing to words absent anywhere in the dictionary were removed (e.g. link to *бу́хта-бара́хта* from *барахта́тися*).

### Languages

Structure:
* `abbreviation`: the abbreviation in the form it (mostly) appears in the dictionary;
* `aliases`: comma-delimited variants of the same abbreviation and other abbreviations applying to the same language;
* `name_uk`: the name of the language in Ukrainian;
* `name_uk_synonym`: an alternative name of the language in Ukrainian;
* `name_en`: the name of the language in English;
* `iso_code`: ISO code of the language if exists.

Notes:
* This database contains not only languages but also their dialects on the one side and whole families on the other. No distinction was made for the reason that the difference is often too subtle.
* There exist abbreviations consisting of several parts, each already included in the list. In such cases, the ones used often (e.g. *ар.-перс.* for Arabo-Persian) are included in the list, while the rare ones (e.g. *кит.-кор.* for Sino-Korean) aren't.
* The spelling of some language names in Ukrainian was changed according to current spelling norms (e.g. *карібська* -> *карибська*, *кумикська* -> *кумицька*).

### Abbreviations

Structure:
* `abbreviation`: the abbreviation in the form it (mostly) appears in the dictionary;
* `aliases`: comma-delimited variants of the same abbreviation and other abbreviations applying to the same term;
* `type`: one of the following types of the term abbreviated:
    * `meta`: etymology and navigation;
    * `pos`: parts of speech;
    * `grammar`: other grammatical concepts;
    * `misc`: other common abbreviations;
* `meaning_uk`: the meaning of the abbreviation in Ukrainian;
* `meaning_en`: the meaning of the abbreviation in English.

Note:
* Similar abbreviations appear here and in the [Languages](#languages) section (e.g. *ос.* may refer either to *особа* '(grammatical) person' or to *осетинська* 'Ossetian').

## What has been done

* Added some missing articles (e.g. *че́знути*) and missing article parts (e.g. for *бі́лий*).
* Amplified the list of language abbreviations: the web version missed those listed in volume 6 and the paper version itself missed some of the rarely used ones (e.g. Javanese).
* Compiled a list of abbreviations used in the dictionary: for the most part, it is the list, parts of which were given at the beginning of the dictionary's volumes, but some other common abbreviations were added as well.
* Processed links which weren't parsed (e.g. *соба́ка* in *собачи́на* article).
* In cases when the article was giving several links in the etymology section, only the last one was initially processed. Here others were added as well (e.g. *же́вріти* in *зе́вриво* article).
* Corrected splitting of the articles into parts (see, for example, *авіа-*).
* Removed duplicate text (see, for example, *де-*).
* Removed parts of the literature section which were incorrectly classified as etymology (see, for example, *гіпе́рбола*).
* Added missing and corrected wrong opening/closing brackets and quotation marks – some were absent or wrong in the original text, some were lost in the process of OCR.
* Corrected punctuation where it was OCRed wrongly (e.g. *р- болг.* -> *р. болг.* at *Бори́с*).
* Corrected italicization of words and phrases in Cyrillic script (e.g. `ґайдува́<I>ти</I>` -> `<I>ґайдува́ти</I>`, `<I>ні</I> <I>стейки</I>, <I>ні</I> <I>гейки</I>` –> `<I>ні стейки, ні гейки</I>`).
* Corrected some wrongly displayed characters (Belarusian ў, Czech ť, accents, etc.).
* Replaced characters from wrong scripts (Greek *νκρ.* in place of Cyrillic *укр.*, a mix *үаү7раьга* in place of Greek *γάγγραινα*, etc.).
* Removed hyphenation and spaces in words which were torn apart by line breaks (e.g. *ре-  зультат* at *боро́да́вка*) and returned hyphens which were treated as hyphenation at line breaks (e.g. *хліборобівукраїнців* in *Григо́рій*).
* Corrected occasional OCR 'typos', sometimes combined with other common issues (e.g. `<I>більшсвизу</I> –  <I>ва́ти</I>` -> `<I>більшовизува́ти</I>`).
* Corrected occasional upper case, introduced by OCR (e.g. *КОЛТУННИК* in *баранець*).
* Added missing italics (e.g. for Slavic counterparts written in Cyrillic in *ріка́* article).

Notes:
* HTML syntax present in the articles: `<I>` for italic, `<B>` for bold (OCRed rather inconsistently), `<SUP>` for superscript, `<SUB>` for subscript.
* Instead of the < and > characters ‹ and › are used.
* It's highly likely that there can still be found a lot of wrong characters (especially in the Greek text), typos and wrong punctuation. Pointing out any of them would be highly appreciated.