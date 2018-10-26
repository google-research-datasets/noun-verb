# Noun Verb Dataset

This dataset contains naturally-occurring English sentences that feature
non-trivial noun-verb ambiguity.

## Motivation

English part-of-speech taggers regularly make egregious errors related to
noun-verb ambiguity, despite having achieved 97%+ accuracy on the WSJ Penn
Treebank since 2002. These mistakes have been difficult to quantify and make
taggers less useful to downstream tasks such as translation and text-to-speech
synthesis.

Below are some examples from the dataset:

1. Certain insects can damage plumerias, such as mites, **flies**, or aphids.
*NOUN*
2. **Mark** which area you want to distress. *VERB*

All tested existing part-of-speech taggers mistag both of these examples,
tagging *flies* as a verb and *Mark* as a noun.

## Description

The dataset contains sentences in CoNLL format. Each sentence has a single token
that has been manually annotated as either VERB or NON-VERB. The sentences
come from multiple domains. Where applicable, the url of the source page
for the sentence is included in a comment line before the sentence.

The dataset is split into Train/Dev/Test sections. For Dev and Test sections the
annotations included either VERB or NON-VERB in XPOS, UPOS and FEATS columns.
For the Train section, XPOS and UPOS columns are replaced with a (predicted)
fine POS tag obtained by running automatic tagger and selecting the top tag that
matched the gold coarse-grained VERB/NON-VERB label.

An example of a training sentence is shown below:

```
# https://www.wikihow.com/Not-Get-Bored-on-a-Long-Car-Ride
1   License _   NN  NN  POS=NON-VERB|fPOS=NON-VERB  -1  _   _   _
2   plates  _   _   _   _   -1  _   _   _
3   of  _   _   _   _   -1  _   _   _
4   cars    _   _   _   _   -1  _   _   _
5   from    _   _   _   _   -1  _   _   _
6   your    _   _   _   _   -1  _   _   _
7   area    _   _   _   _   -1  _   _   _
8   or  _   _   _   _   -1  _   _   _
9   your    _   _   _   _   -1  _   _   _
10  destination _   _   _   _   -1  _   _   _
11  .   _   _   _   _   -1  _   _   _

```

The number of examples are shown below:

           | Train     | Dev      | Test
:--------- | --------: | -------: | -------:
Total      | 23458     | 2367     | 5907

These numbers are slightly lower than those reported in Table 5 of the
[paper](#citation) by 796, 33, and 93 examples, respectively.

## Updated Results

We reran the experiments reported in Tables 1 and 9 of the [paper](#citation)
using the slightly filtered data. The updated results are reported as means and
standard deviations based on an average of 10 runs:

Model           | WSJ            | NV           | Homographs (Micro) | Homographs (Macro)
:-------------- | -------------: | -----------: | -----------------: | -----------------:
WSJ             | **98.07±0.06** | 73.9±1.5     | 95.7±0.3           | 95.8±0.3
WSJ+ELMo        | 97.99±0.06     | 81.5±1.1     | **96.8±0.2**       | **96.8±0.2**
WSJ+Silver      | 98.00±0.07     | 86.4±0.5     | 96.0±0.2           | 96.1±0.2
WSJ+ELMo+Silver | 98.01±0.06     | **88.7±0.4** | **96.7±0.2**       | **96.8±0.2**

An updated version of Table 7, tuned on the Noun-Verb development set, is as
follows:

Model           | WSJ            | NV
:-------------- | -------------: | -----------:
WSJ             | **98.03±0.10** | 76.9±0.5
WSJ+ELMo        | 97.90±0.09     | 83.4±0.3
WSJ+Silver      | **97.97±0.09** | 87.1±0.3
WSJ+ELMo+Silver | 97.95±0.08     | **89.1±0.2**

## Contact

If you have a technical question regarding the dataset or publication, please
create an issue in this repository.

## Citation

If you use or discuss this dataset in your work, please cite our paper:

```
@InProceedings{NOUNVERB,
  title = {A Challenge Set and Methods for Noun-Verb Ambiguity},
  author = {Ali Elkahky and Kellie Webster and Daniel Andor and Emily Pitler},
  booktitle = {Proceedings of EMNLP},
  year = {2018}
}
```
