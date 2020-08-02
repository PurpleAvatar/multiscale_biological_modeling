---
permalink: /motifs/finding
title: "Finding Network Motifs"
sidebar:
 nav: "motifs"
---

## Loops in the TF network

* At the end of the previous section, we introduced transcription factor network and saw that this network for *E. coli* had what appeared to be a large number of loops (i.e., edges connecting a node *X* to itself).

* The question, however, is whether seeing this many loops in the transcription factor network means that the loop is an important feature of this network.

* Throughout computational biology, a fundamental paradigm when determining whether some structure is significant is to ask how likely this structure would be to appear as the result of *randomness* --- once again, using randomness to answer practical questions rears its head. The approach of quantifying the significance of an object by comparing its likelihood of appearing within randomly will not be foreign to anyone who is familiar with the search tool BLAST, which evaluates the matches that it finds of a query against a database by quantifying the likelihood that we would see this query within a random database.

* In this case, we will determine whether loops in transcription factor networks are significant by comparing the number of loops in the *E. coli* network against the number of loops in a randomly generated transcription factor network. If the number of loops in the *E. coli* network is much higher than the expected number of loops in the randomly generated network, then we know that loops most likely have not appeared because of random chance (and must therefore appear frequently within the transcription factor network for a reason).

* START HERE -- introduction to Jupyter notebook walkthrough.

*Each node (repr. gene) can be connected to other genes, and we can break down into these simple arrangements*

*Picture of simplest patterns, A -> B, A -| B, A -| A, etc*

## Jupyter Notebook Walkthrough

CITE

[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](nar){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
