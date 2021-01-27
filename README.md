# Modern Standard Arabic (arb)

This repo contains the inflection tables for Modern Standard Arabic (ISO 639-3 `arb`)

## Contents
- `ara`: UniMorph previously existing data (from Wiktionary English).
- `ara_atb`: entries based on lemmas that appear in the Penn Arabic Treebank (PATB).
- `ara_atb.gloss`: English glosses for the lemmas in `ara_atb`.
- `ara_new`: entries based on a subset of `ara` processed in the same manner as
  in `ara_atb`.
- `ara_new.gloss`: English glosses for the lemmas in `ara_new`.
- `README.md`: this file.

#

## `ara_atb`

### Generation of the lemma inflections
- The inflections of all the lemmas were generated through the CamelTools morphological generator component
  ([demo](https://calimastar.abudhabi.nyu.edu/generator),
  [API](https://camel-tools.readthedocs.io/en/latest/api/morphology/generator.html))
  ([Obeid et al., 2020](https://www.aclweb.org/anthology/2020.lrec-1.868v2.pdf)).
  The morphological database used is CalimaStar ([Taji et al.](https://www.aclweb.org/anthology/W18-5816/)).
- The POS and morphological features are then mapped to UniMorph according to
  the current [schema](https://unimorph.github.io/doc/unimorph-schema.pdf)
  (Sylak-Glassman 2016).
- The core POS of the lemmas are Verbs, Nouns, and Adjectives (following the
  same categories in `ara`).
- The total number of lemmas is 13,049, with the following POS distribution:
    - `V`: 2,610 (20.0%) lemmas
    - `N`: 7,367 (56.5%) lemmas
    - `ADJ`: 3,072 (23.5%) lemmas

### Source
- PATB treebanks: All the lemmas in both PATB ([Maamouri et at. 2004](https://www.marefa.org/images/e/e8/The_penn_arabic_treebank_Building_a_large-scale_an_%281%29.pdf))
      and in CalimaStar.

### Notes on Tokenization and Diacritization
- Clitics were not included or marked in the inflection tables. The only clitic
  included is the determiner `Al+` in order to be consistent with both PATB and
  the [Arabic UD](https://github.com/UniversalDependencies/UD_Arabic-NYUAD).
- All the lemmas and the inflected forms are fully diacritized following the
  same convention in the PATB. Removing all the diacritics is straightforward and
  can be done through a simple regex. Alternatively, CamelTools provides a
  dediacritization utility: an
  [API](https://camel-tools.readthedocs.io/en/latest/api/utils/dediac.html)
 and a [CLI](https://camel-tools.readthedocs.io/en/latest/cli/camel_dediac.html).

### Notes on POS decisions
- Definiteness and Possession:
    - In MSA, a nominal's state can be `definite`, `indefinite`, or
      `construct`. Nominals can take determiner particle `Al+`. Not all determiner and state values are allowed. Indefinite nouns and adjectives, as well as construct nouns, cannot take the determiner; however, a construct adjectives can appear in a special construction (False Idafa) where they can take the determiner. Also, nouns can be definite without the determiner ([Smrž 2007](https://dspace.cuni.cz/bitstream/handle/20.500.11956/13736/140015347.pdf)).
    - In UniMorph, Definiteness and Possession are two separate   dimensions.
      Therefore, to map MSA linguistic facts to UniMorph, we take the following approach:
        - When no `Al+` is present, MSA’s `definite`, `indefinite`, or
          `construct` state will be mapped to `SPEC`, `INDEF`, and `PSSD`,
          respectively.
        - When `Al+` is present with a `definite` nominal, we use `DEF`.
        - When `Al+` is present with a `construct` adjective, the adjective will be tagged with both `DEF` and `PSSD` for definiteness and possession respectively.
- Aspect and Mood:
    - MSA verbs can be `perfective`, `imperfective` or `imperative` (often
      marked as their aspect);  an imperfective verb can be `indicative`,
      `subjunctive`, or `jussive`.
    - UniMorph has a single mood tag `IMP` which conflates both `imperative`
      and `jussive` feature values.
    - To resolve this incompatibility, we suggest splitting the
      `imperative-jussive` tag into two tags `imperative` (`IMP`) and `jussive`
      (`JUS`) and that is what we used in the tables we generated.
#
## `ara_new`

### Description:
The lemmas in `ara_new` are a subset of the lemmas that appear `ara` inflected
in a way consistent with `ara_atb`. The lemmas in `ara` are not diacritized and
have no associated gloss, so we mapped them to their equivalant diacritized
lemmas in CalimaStar. We were able to extract 3,084 (74.8%) out of 4,126
lemmas. The inflection process is described
[above](#Generation-of-the-lemma-inflections). In total there are 3,562
lemmas with the following POS distribution: 
- `V`: 661 (18.6%) lemmas
- `N`: 2,522 (70.8%) lemmas
- `ADJ`: 379 (10.6%) lemmas
#
## Annotators
Salam Khalifa and Nizar Habash ([CAMeL Lab](www.camel-lab.com) @ NYU Abu Dhabi)

## Paradigm Samples
The complete inflection table for the adjective lemma مُتَّحِد _'united'_

```
مُتَّحِد	المُتَّحِدَتَيْنِ	ADJ;ACC;DEF;FEM;DU
مُتَّحِد	المُتَّحِدَتَيْ	ADJ;ACC;DEF;FEM;DU;PSSD
مُتَّحِد	المُتَّحِداتِ	ADJ;ACC;DEF;FEM;PL
مُتَّحِد	المُتَّحِداتِ	ADJ;ACC;DEF;FEM;PL;PSSD
مُتَّحِد	المُتَّحِدَةَ	ADJ;ACC;DEF;FEM;SG
مُتَّحِد	المُتَّحِدَةَ	ADJ;ACC;DEF;FEM;SG;PSSD
مُتَّحِد	المُتَّحِدَيْنِ	ADJ;ACC;DEF;MASC;DU
مُتَّحِد	المُتَّحِدَيْ	ADJ;ACC;DEF;MASC;DU;PSSD
مُتَّحِد	المُتَّحِدِينَ	ADJ;ACC;DEF;MASC;PL
مُتَّحِد	المُتَّحِدِي	ADJ;ACC;DEF;MASC;PL;PSSD
مُتَّحِد	المُتَّحِدَ	ADJ;ACC;DEF;MASC;SG
مُتَّحِد	المُتَّحِدَ	ADJ;ACC;DEF;MASC;SG;PSSD
مُتَّحِد	مُتَّحِدَتَيْ	ADJ;ACC;FEM;DU;PSSD
مُتَّحِد	مُتَّحِداتِ	ADJ;ACC;FEM;PL;PSSD
مُتَّحِد	مُتَّحِدَةَ	ADJ;ACC;FEM;SG;PSSD
مُتَّحِد	المُتَّحِدَتَيْنِ	ADJ;ACC;INDF;FEM;DU
مُتَّحِد	مُتَّحِدَتَيْنِ	ADJ;ACC;INDF;FEM;DU
مُتَّحِد	مُتَّحِداتٍ	ADJ;ACC;INDF;FEM;PL
مُتَّحِد	مُتَّحِدَةً	ADJ;ACC;INDF;FEM;SG
مُتَّحِد	مُتَّحِدَيْنِ	ADJ;ACC;INDF;MASC;DU
مُتَّحِد	مُتَّحِدِينَ	ADJ;ACC;INDF;MASC;PL
مُتَّحِد	مُتَّحِداً	ADJ;ACC;INDF;MASC;SG
مُتَّحِد	مُتَّحِدَيْ	ADJ;ACC;MASC;DU;PSSD
مُتَّحِد	مُتَّحِدِي	ADJ;ACC;MASC;PL;PSSD
مُتَّحِد	مُتَّحِدَ	ADJ;ACC;MASC;SG;PSSD
مُتَّحِد	مُتَّحِدَتَيْ	ADJ;ACC;SPEC;FEM;DU
مُتَّحِد	مُتَّحِدَتَيْنِ	ADJ;ACC;SPEC;FEM;DU
مُتَّحِد	مُتَّحِداتِ	ADJ;ACC;SPEC;FEM;PL
مُتَّحِد	مُتَّحِدَةَ	ADJ;ACC;SPEC;FEM;SG
مُتَّحِد	مُتَّحِدَيْ	ADJ;ACC;SPEC;MASC;DU
مُتَّحِد	مُتَّحِدَيْنِ	ADJ;ACC;SPEC;MASC;DU
مُتَّحِد	مُتَّحِدِي	ADJ;ACC;SPEC;MASC;PL
مُتَّحِد	مُتَّحِدِينَ	ADJ;ACC;SPEC;MASC;PL
مُتَّحِد	مُتَّحِدَ	ADJ;ACC;SPEC;MASC;SG
مُتَّحِد	المُتَّحِدات	ADJ;DEF;FEM;PL
مُتَّحِد	المُتَّحِدات	ADJ;DEF;FEM;PL;PSSD
مُتَّحِد	المُتَّحِدَة	ADJ;DEF;FEM;SG
مُتَّحِد	المُتَّحِدَة	ADJ;DEF;FEM;SG;PSSD
مُتَّحِد	المُتَّحِد	ADJ;DEF;MASC;SG
مُتَّحِد	المُتَّحِد	ADJ;DEF;MASC;SG;PSSD
مُتَّحِد	مُتَّحِدات	ADJ;FEM;PL;PSSD
مُتَّحِد	مُتَّحِدَة	ADJ;FEM;SG;PSSD
مُتَّحِد	المُتَّحِدَتَيْنِ	ADJ;GEN;DEF;FEM;DU
مُتَّحِد	المُتَّحِدَتَيْ	ADJ;GEN;DEF;FEM;DU;PSSD
مُتَّحِد	المُتَّحِداتِ	ADJ;GEN;DEF;FEM;PL
مُتَّحِد	المُتَّحِداتِ	ADJ;GEN;DEF;FEM;PL;PSSD
مُتَّحِد	المُتَّحِدَةِ	ADJ;GEN;DEF;FEM;SG
مُتَّحِد	المُتَّحِدَةِ	ADJ;GEN;DEF;FEM;SG;PSSD
مُتَّحِد	المُتَّحِدَيْنِ	ADJ;GEN;DEF;MASC;DU
مُتَّحِد	المُتَّحِدَيْ	ADJ;GEN;DEF;MASC;DU;PSSD
مُتَّحِد	المُتَّحِدِينَ	ADJ;GEN;DEF;MASC;PL
مُتَّحِد	المُتَّحِدِي	ADJ;GEN;DEF;MASC;PL;PSSD
مُتَّحِد	المُتَّحِدِ	ADJ;GEN;DEF;MASC;SG
مُتَّحِد	المُتَّحِدِ	ADJ;GEN;DEF;MASC;SG;PSSD
مُتَّحِد	مُتَّحِدَتَيْ	ADJ;GEN;FEM;DU;PSSD
مُتَّحِد	مُتَّحِداتِ	ADJ;GEN;FEM;PL;PSSD
مُتَّحِد	مُتَّحِدَةِ	ADJ;GEN;FEM;SG;PSSD
مُتَّحِد	المُتَّحِدَتَيْنِ	ADJ;GEN;INDF;FEM;DU
مُتَّحِد	مُتَّحِدَتَيْنِ	ADJ;GEN;INDF;FEM;DU
مُتَّحِد	مُتَّحِداتٍ	ADJ;GEN;INDF;FEM;PL
مُتَّحِد	مُتَّحِدَةٍ	ADJ;GEN;INDF;FEM;SG
مُتَّحِد	مُتَّحِدَيْنِ	ADJ;GEN;INDF;MASC;DU
مُتَّحِد	مُتَّحِدِينَ	ADJ;GEN;INDF;MASC;PL
مُتَّحِد	مُتَّحِدٍ	ADJ;GEN;INDF;MASC;SG
مُتَّحِد	مُتَّحِدَيْ	ADJ;GEN;MASC;DU;PSSD
مُتَّحِد	مُتَّحِدِي	ADJ;GEN;MASC;PL;PSSD
مُتَّحِد	مُتَّحِدِ	ADJ;GEN;MASC;SG;PSSD
مُتَّحِد	مُتَّحِدَتَيْ	ADJ;GEN;SPEC;FEM;DU
مُتَّحِد	مُتَّحِدَتَيْنِ	ADJ;GEN;SPEC;FEM;DU
مُتَّحِد	مُتَّحِداتِ	ADJ;GEN;SPEC;FEM;PL
مُتَّحِد	مُتَّحِدَةِ	ADJ;GEN;SPEC;FEM;SG
مُتَّحِد	مُتَّحِدَيْ	ADJ;GEN;SPEC;MASC;DU
مُتَّحِد	مُتَّحِدَيْنِ	ADJ;GEN;SPEC;MASC;DU
مُتَّحِد	مُتَّحِدِي	ADJ;GEN;SPEC;MASC;PL
مُتَّحِد	مُتَّحِدِينَ	ADJ;GEN;SPEC;MASC;PL
مُتَّحِد	مُتَّحِدِ	ADJ;GEN;SPEC;MASC;SG
مُتَّحِد	مُتَّحِدات	ADJ;INDF;FEM;PL
مُتَّحِد	مُتَّحِدَة	ADJ;INDF;FEM;SG
مُتَّحِد	مُتَّحِد	ADJ;INDF;MASC;SG
مُتَّحِد	المُتَّحِدَتانِ	ADJ;NOM;DEF;FEM;DU
مُتَّحِد	المُتَّحِدَتا	ADJ;NOM;DEF;FEM;DU;PSSD
مُتَّحِد	المُتَّحِداتُ	ADJ;NOM;DEF;FEM;PL
مُتَّحِد	المُتَّحِداتُ	ADJ;NOM;DEF;FEM;PL;PSSD
مُتَّحِد	المُتَّحِدَةُ	ADJ;NOM;DEF;FEM;SG
مُتَّحِد	المُتَّحِدَةُ	ADJ;NOM;DEF;FEM;SG;PSSD
مُتَّحِد	المُتَّحِدانِ	ADJ;NOM;DEF;MASC;DU
مُتَّحِد	المُتَّحِدا	ADJ;NOM;DEF;MASC;DU;PSSD
مُتَّحِد	المُتَّحِدُونَ	ADJ;NOM;DEF;MASC;PL
مُتَّحِد	المُتَّحِدُو	ADJ;NOM;DEF;MASC;PL;PSSD
مُتَّحِد	المُتَّحِدُ	ADJ;NOM;DEF;MASC;SG
مُتَّحِد	المُتَّحِدُ	ADJ;NOM;DEF;MASC;SG;PSSD
مُتَّحِد	مُتَّحِدَتا	ADJ;NOM;FEM;DU;PSSD
مُتَّحِد	مُتَّحِداتُ	ADJ;NOM;FEM;PL;PSSD
مُتَّحِد	مُتَّحِدَةُ	ADJ;NOM;FEM;SG;PSSD
مُتَّحِد	مُتَّحِدَتانِ	ADJ;NOM;INDF;FEM;DU
مُتَّحِد	مُتَّحِداتٌ	ADJ;NOM;INDF;FEM;PL
مُتَّحِد	مُتَّحِدَةٌ	ADJ;NOM;INDF;FEM;SG
مُتَّحِد	مُتَّحِدانِ	ADJ;NOM;INDF;MASC;DU
مُتَّحِد	مُتَّحِدُونَ	ADJ;NOM;INDF;MASC;PL
مُتَّحِد	مُتَّحِدٌ	ADJ;NOM;INDF;MASC;SG
مُتَّحِد	مُتَّحِدا	ADJ;NOM;MASC;DU;PSSD
مُتَّحِد	مُتَّحِدُو	ADJ;NOM;MASC;PL;PSSD
مُتَّحِد	مُتَّحِدُ	ADJ;NOM;MASC;SG;PSSD
مُتَّحِد	مُتَّحِدَتانِ	ADJ;NOM;SPEC;FEM;DU
مُتَّحِد	مُتَّحِداتُ	ADJ;NOM;SPEC;FEM;PL
مُتَّحِد	مُتَّحِدَةُ	ADJ;NOM;SPEC;FEM;SG
مُتَّحِد	مُتَّحِدا	ADJ;NOM;SPEC;MASC;DU
مُتَّحِد	مُتَّحِدانِ	ADJ;NOM;SPEC;MASC;DU
مُتَّحِد	مُتَّحِدُو	ADJ;NOM;SPEC;MASC;PL
مُتَّحِد	مُتَّحِدُونَ	ADJ;NOM;SPEC;MASC;PL
مُتَّحِد	مُتَّحِدُ	ADJ;NOM;SPEC;MASC;SG
مُتَّحِد	مُتَّحِدات	ADJ;SPEC;FEM;PL
مُتَّحِد	مُتَّحِدَة	ADJ;SPEC;FEM;SG
```
## License
- [Creative Commons Attribution-ShareAlike 3.0 Unported (CC BY-SA 3.0)](https://creativecommons.org/licenses/by-sa/3.0/)
