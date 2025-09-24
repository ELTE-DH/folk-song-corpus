# ELTE Folk Song Corpus


ELTE Folk Song Corpus is a database developed by the [_Department of Digital Humanities at Eötvös Loránd University_](https://elte-dh.hu/). Currently, the corpus contains 2390 Hungarian folk songs, the sound devices of the texts and the grammatical features of words in XML format (in TEI and non-TEI XML format).

## Size

- number of folk songs: 2390
- number of words: 113 565
- number of tokens: 148 524

## TEI Levels

The source of the corpus was the digital version of the book Magyar népdalok (Hungarian Folk Songs) edited and selected by Gyula Ortutay and Imre Katona, published in 1976. The HTML files of the book were downloaded from the [_Hungarian Electronic Library_](http://mek.oszk.hu).

1. The HTML files from the Hungarian Electronic Library were converted into TEI XML format based on the [_Text Encoding Initiative_](https://tei-c.org/).
3. Then, we tokenized the poems and annotated the grammatical features of words by using [_e-magyar_](https://github.com/nytud/emtsv), an NLP tool chain for Hungarian texts. The level2 folder contains the TEI XML files in which the morphosyntactic features (values of the msd attributes) are annotated in the format of universal dependencies, while the level2\_emMorph folder contains the same files in which the morphosyntactic features are annotated in its own, [_emMorph_](https://e-magyar.hu/en/textmodules/emmorph_codelist) format of e-magyar.
4. After the grammatical annotation, we also annotated the rhyme patterns, the rhyme pairs, the rhythm of lines, the alliterations, the phonological features of words, and the meters of the folk songs (level3).
5. Finally, we added further annotations of poetic features to the corpus and changed the name and the position of some elements and attributes, using a non-TEI XML format defined for the project (level4).

# Elements and attributes

## Level1 -- annotation of structural units

- `<head>` : title
- `<lg>`: stanza
- `<l>`: line
- `<p>`: subtitle, epigraph, separator, editorial note


## Level2 -- tokenization and annotation of grammatical features of words

- `<w>` : word
- `<pc> `: punctuation mark
- `@lemma` : lemma
- `@pos `: part of speech
- `@msd` : morphosyntactic features ([Universal Dependencies](https://universaldependencies.org/))


## Level3_without_meter -- annotation of sound devices without meter

The same as level3 without the `@met` attribute containing the meter of the folk songs. This is the input format of the program Hunpoem\_meter\_analyzer detecting quantitative and qualitative meter in Hungarian poetry.


## Level3 -- annotation of sound devices

- `@met `: meter
	- `Qual` : qualitative meter based on stressed and unstressed syllables
	- `Quan` : quantitative meter based on long and short syllables (possible values: iambic, trochaic, dactylic, anapestic)
	- `QuanScore` : score of quantitative meter (before 0.5, the poem does not really have any intended quantitative meter)
- `@rhyme `: rhyme pattern
- `@real `: rhythm (0: short syllable; 1: long syllable)
- `<spanGrp type="phonStructures">` : standoff annotation of the phonological features of words
- `<span>` : standoff annotation of the phonological features of a word
	content of `<span>` : phonological representation of the word
	- `c`: consonant
	- `b`: short back vowel
	- `B`: long back vowel
	- `f`: short front vowel
	- `F`: long front vowel
- `@subtype` : syllable number
- `@type` : type of vowels
	- `low`: only back vowels in the word
	- `high`: only front vowels in the word
	- `mixed`: front and back vowels in the word
- `@target` : the `xml:id` of the annotated word
- `<linkGrp type="rhymePairs">` : standoff annotation of rhyme pairs
- `<link>` : standoff annotation of a rhyme pair
- `@target` : xml:id of the two words in a rhyme pair
- `<spanGrp type="alliterations">` : standoff annotation of alliterations
- `<span>` : standoff annotation of an alliteration
- `@target` : `xml:id` of the words in the alliteration
- `@type` : structure of the alliteration
	- `a`: alliterating word
	- `n`: non-alliterating word (only one non-alliterating word can be between two alliterating words)

## Level4 -- conversion of the TEI format into non-TEI format 

By changing the name and the position of certain elements and attributes in level3 and by adding further annotations to the corpus, it is easier to process but cannot be expressed in valid TEI XML format.

- `@met_qual` : qualitative meter based on stressed and unstressed syllables (conversion of level3's `@met` in `<div>`)
- `@met_quan` : quantitative meter based on long and short syllables, possible values: iambic, trochaic, dactylic, anapestic (conversion of level3's `@met` in `<div>`)
- `@met_quanScore` : score of quantitative meter, before 0.5, the poem does not really have any intended quantitative meter (conversion of level3's `@met` in `<div>`)
- `@div_numStanza` : number of stanzas in the poem
- `@div_numLine `: number of lines in the poem
- `@div_numWord `: number of words in the poem
- `@div_numSyll `: number of syllables in the poem
- `@div_numShortSyll` : number of short syllables in the poem
- `@div_numLongSyll `: number of long syllables in the poem
- `@div_rhyme` : the rhyme pattern of the poem
- `@div_syllPattern` : syllable numbers of lines in the poem
- `@lg_numLine `: number of lines in the stanza
- `@lg_numWord `: number of words in the stanza
- `@lg_numSyll `: number of syllables in the stanza
- `@lg_numShortSyll` : number of short syllables in the stanza
- `@lg_numLongSyll `: number of long syllables in the stanza
- `@lg_syllPattern `: syllable numbers of lines in the stanza
- `@l_numWord `: number of words in the line
- `@l_numSyll `: number of syllables in the line
- `@l_numShortSyll` : number of short syllables in the line
- `@l_numLongSyll `: number of long syllables in the line 
- `@w_numSyll` : syllable number of word (conversion of level3's `@subtype` in `<span>`)
- `@phonType` : type of vowels in the word (conversion of level3's `@type` in `<span>`)
- `@phonStruct` : phonological representation of the word (conversion of level3's `<span>` content)
- `<rhymePairs> `: standoff annotation of rhyme pairs (conversion of level3's `<linkGrp type="rhymePairs">`)
- `<rhymePair>` : standoff annotation of a rhyme pair (conversion of level3's `<link>`)
- `<firstRhyme>`, `<secondRhyme>` : standoff annotation of the first and second word of a rhyme pair
	- content of `<firstRhyme>` and `<secondRhyme>` : the rhyming word form
- `@rhyme_lemma` : the lemma of the rhyming word
- `@rhyme_pos` : the part of speech of the rhyming word
- `@rhyme_msd` : the morphosyntactic features of the rhyming word (Universal Dependencies)
- `@rhyme_numSyll` : the syllable number of the rhyming word
- `@rhyme_phonType `: the type of vowels in the rhyming word
- `@rhyme_phonStruct` : the phonological representation of the rhyming word
- `<alliterations>` : standoff annotation of alliterations (conversion of level3's `<spanGrp type="alliterations">`)
- `<alliteration>` : standoff annotation of an alliteration (conversion of level3's `<span>`)
	- content of `<alliteration>` : the alliterating word forms
- `@allStruct` : structure of the alliteration (conversion of level3's `@type` in `<span>`)
- `@posTags` : the parts of speech of the alliterating words
- `@msdTags `: the morphosyntactic features of the alliterating words
- `@lemmas` : the lemmas of the alliterating words


# Contributors

- [Péter Horváth](https://github.com/horvathpeti99) (design, annotation scripts)
- [Gábor Palkó](https://github.com/luhpeg) (design, data model)


# Citing and license

If you use ELTE Folksong Corpus, please cite the following article:

Horváth Péter – Kundráth Péter – Palkó Gábor 2022. ELTE Népdalkorpusz – magyar népdalok gépileg annotált adatbázisa. In: Tick József – Kokas Károly – Holl András (szerk.): Valós térben – Az online térért: Networkshop 31: országos konferencia. Budapest: HUNGARNET Egyesület. 276-283.

The content of the repository is licensed under the [CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/) license.

All texts of the corpus are in the public domain.



