---
permalink: /motifs/finding
title: "Finding Network Motifs"
sidebar:
 nav: "motifs"
---

## Loops in the TF network

In the previous section, we introduced biological networks, in particular the transcription factor network, in which a protein *X* is connected to a protein *Y* if *X* is a transcription factor that regulates the production of *Y*. We also saw that in the *E. coli* transcription factor network, there seemed to be a large number of loops (i.e., edges connecting a node to itself).

However, we need a more rigorous approach to arguing that there are many loops than simply observing the network. The question is how to justify quantitatively that the loop is a frequently used network motif.

To answer this question, we will apply a paradigm that occurs throughout computational biology (and  science in general) for determining whether an observation is significant. This approach asks how likely this observation would have been made in a *random* environment --- once again we see the power of randomness for answering practical questions.

For a classic example, many biologists are familiar with the search tool [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi){:target="_blank"}, which allows researchers to compare a query (say, the DNA sequence of a newly sequenced gene) against a database to find whether the query appears with slight modifications in the database. Once BLAST finds a "hit" of the query in the database, it asks "What are the chances we would find a hit of this quality in a random database?" If that probability is very low, then we can feel confident that the hit we found is significant.

**STOP:** How can we apply this paradigm to determine whether a transcription factor network contains a significant number of loops?

* In this case, we will determine whether loops in transcription factor networks are significant by comparing the number of loops in the *E. coli* network against the number of loops in a randomly generated transcription factor network. If the number of loops in the *E. coli* network is much higher than the expected number of loops in the randomly generated network, then we know that loops most likely have not appeared because of random chance (and must therefore appear frequently within the transcription factor network for a reason).

* START HERE -- introduction to Jupyter notebook walkthrough.

*Each node (repr. gene) can be connected to other genes, and we can break down into these simple arrangements*

*Picture of simplest patterns, A -> B, A -| B, A -| A, etc*

## Jupyter Notebook Walkthrough

CITE

[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](nar){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
