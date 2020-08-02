---
permalink: /motifs/finding
title: "Finding Network Motifs"
sidebar:
 nav: "motifs"
---

## Using randomness to determine statistical significance

In the previous section, we introduced biological networks, in particular the transcription factor network, in which a protein *X* is connected to a protein *Y* if *X* is a transcription factor that regulates the production of *Y*. We also saw that in the *E. coli* transcription factor network, there seemed to be a large number of loops (i.e., edges connecting a node to itself).

However, we need a more rigorous approach to arguing that there are many loops than simply observing the network. The question is how to justify quantitatively that the loop is a frequently used network motif.

To answer this question, we will apply a paradigm that occurs throughout computational biology (and  science in general) for determining whether an observation is significant. This approach asks how likely this observation would have been made in a *random* environment --- once again we see the power of randomness for answering practical questions.

For a classic example, many biologists are familiar with the search tool [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi){:target="_blank"}, which allows researchers to compare a query (say, the DNA sequence of a newly sequenced gene) against a database to find whether the query appears with slight modifications in the database. Once BLAST finds a "hit" of the query in the database, it asks, "What are the chances we would find a hit of this quality in a random database?" If that probability is very low, then we can feel confident that the hit we found is significant.

**STOP:** How can we apply this paradigm to determine whether a transcription factor network contains a significant number of loops?

## Comparing a real transcription factor network against a random network

We will determine whether there are a significant number of loops in the transcription factor network of *E. coli* by comparing the number of loops that we find in the network against the expected number of loops we would find in a randomly generated network. If the number of loops in the real network is much higher than the number of loops in the random network, then we have strong evidence that there is some selective force causing a loop to be a network motif.

The next question is how to form a random network that offers a reasonable comparison against a real network.

## Forming a random network

There are multiple ways to generate a random network, but we will use an approach developed by Edgar Gilbert in 1959. In this approach, we have are given an integer *n* and a probability *p* (between 0 and 1). We first form *n* nodes; then, for every possible pair of nodes *x* and *y*, we have probability equal to *p* of connecting *x* to *y* with a directed edge *x* → *y*.

CITE:  Gilbert, E.N. (1959). "Random Graphs". Annals of Mathematical Statistics. 30 (4): 1141–1144. doi:10.1214/aoms/1177706098.

**STOP:** What should *n* and *p* be if we are generating a random network to compare against the *E. coli* transcription factor network?

In the spirit of making a fair comparison, we should therefore generate a random network with approximately the same number of nodes and edges. The *E. coli* transcription factor network has XXX total nodes and YYY edges, so we will take *n* = XXX. To ensure that the random network has approximately YYY edges, we first note that there are *n*<sup>2</sup> pairs of nodes that could have an edge connecting them (*n* choices for the starting node and *n* for the ending node). In order to ensure that we have approximately YYY edges in the random network, we set *p* equal to YYY/*n*<sup>2</sup>.  On average, YYY of the number of pairs of nodes that will be selected for an edge is *n*<sup>2</sup>·(YYY/*n*<sup>2</sup>) = YYY.




If you are interested in

[Visit tutorial](tutorial_loops){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}



## Jupyter Notebook Walkthrough

CITE

[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](nar){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
