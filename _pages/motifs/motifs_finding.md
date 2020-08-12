---
permalink: /motifs/finding
title: "How to Find Network Motifs"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## The loop: the simplest network motif

In the previous lesson, we introduced the transcription factor network, in which a protein *X* is connected to a protein *Y* if *X* is a transcription factor that regulates the production of *Y*. We also saw that in the *E. coli* transcription factor network, there seemed to be a large number of loops, corresponding to transcription factor autoregulation.

In the introduction, we briefly mentioned the notion of a network motif, or a structure occurring often throughout a biological network. In the remainder of this chapter, we discuss how to identify network motifs as well as explain why they occur so often in the network. And we will start our work by studying the loop.

## Using randomness to determine statistical significance

We first need to be able to argue rigorously that loops occurs significantly often in the transcription factor network to be called a motif.

To quantify the significance of a candidate motif, we will apply a paradigm that occurs throughout computational biology (and science in general) for determining whether an observation is significant. In this approach, we compare our observation against a  *randomly generated* database --- once again, we see the power of randomness for answering practical questions!

A seminal example of this paradigm from biological research is the search tool [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi), which allows researchers to compare a query (say, the DNA sequence of a newly sequenced gene) against a database (say, a collection of many species' genomes). Once BLAST finds a "hit" of the query occurring with slight modifications within the database, it asks, "What is the probability we would find a hit of the same similarity quality in a randomly generated 'decoy' database?" If this probability is low, then we can feel confident that the hit is significant.

**STOP:** How can we apply this paradigm to determine whether a transcription factor network contains a significant number of loops?
{: .notice--primary}

## Comparing a real transcription factor network against a random network

We will determine whether there are a significant number of loops in the transcription factor network of *E. coli* by comparing the number of loops that we find in the network against the expected number of loops we would find in a randomly generated network. If the number of loops in the real network is much higher than the number of loops in the random network, then we have strong evidence that there is some selective force causing a loop to be a network motif.

There are multiple ways to generate a random network, but we will use an approach developed by Edgar Gilbert in 1959. In this approach, we have are given an integer *n* and a probability *p* (between 0 and 1). We first form *n* nodes; then, for every possible pair of nodes *X* and *Y*, we have probability equal to *p* of connecting *X* to *Y* with a directed edge.

* NOAH: please cite:  Gilbert, E.N. (1959). "Random Graphs". Annals of Mathematical Statistics. 30 (4): 1141–1144. doi:10.1214/aoms/1177706098.

**STOP:** What should *n* and *p* be if we are generating a random network to compare against the *E. coli* transcription factor network?
{: .notice--primary}

* NOAH: somewhere cite the RegulonDB network -- presumably in a tutorial. Also give students the full network.

The full *E. coli* transcription factor network includes thousands of genes, most of which are not transcription factors. As a result, the approach described above may form a random network that connects non-transcription factors to other nodes, which we should avoid.

Instead, we will focus on the network comprising only *E. coli* transcription factors that regulate each other. This network has 197 nodes and 477 edges, and so we will begin by forming a random network with *n* = 197 nodes.

We then want to select *p* to ensure that our random network will on average have 477 edges. To do so, we note that there are *n*<sup>2</sup> pairs of nodes that could have an edge connecting them (*n* choices for the starting node and *n* for the ending node). If we were to set *p* equal to 1/*n*<sup>2</sup>, then we would expect on average only to see a single edge in the random network. We therefore scale this value by 477 and set *p* equal to 477/*n*<sup>2</sup>.

We are now ready to build a random network and compare the number of loops in this network with the number of loops in the real transcription factor network. If you'd like, the link below will take you to a short tutorial that includes a Jupyter notebook running this comparison that you can play around with yourself. Otherwise, feel free to skip ahead to the next section.

[Visit tutorial](tutorial_loops){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Negative and positive autoregulation

* In a random network, we would expect about half of the edges to be assigned a "+", and about half of the edges to be assigned a "-".

* Re-examining the 130 total loops in the *E. coli* transcription factor network, we see that AAA of them are assigned a "+" and BBB of them are assigned a "-".

* This enormous discrepancy is doubtfully due to random chance; imagine if we flipped a coin 130 times and obtained AAA "heads" and BBB "tails".

* In other words, we have found that autoregulation is an important aspect of transcription factors, but we have also found that transcription factors that autoregulate tend to *negatively* autoregulate, meaning that they serve to *turn off* their own expression.

* This seems to have taken an even stranger turn --- why in the world would negative autoregulation be such a common phenomenon in transcription factors? In the next section, we will begin to unravel the mystery.

* Define: negative autoregulation

[Next lesson](nar){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
