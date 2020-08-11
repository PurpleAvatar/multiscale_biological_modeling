---
permalink: /motifs/finding
title: "How to Find Network Motifs"
sidebar:
 nav: "motifs"
---

## Using randomness to determine statistical significance

In the previous section, we introduced biological networks, in particular the transcription factor network, in which a protein *X* is connected to a protein *Y* if *X* is a transcription factor that regulates the production of *Y*. We also saw that in the *E. coli* transcription factor network, there seemed to be a large number of loops, in which a transcription factor regulates its own transcription.

A structure occurring often throughout a biological network is called a **network motif**. In the remainder of this chapter, we focus on identifying motifs in transcription factor networks and then trying to find an evolutionary justification for why these motifs are so common.

We first need to be able to argue rigorously that a given structure within a network occurs significantly often to be called a motif. That is, we will need to place our argument on firm statistical footing.

To quantify the significance of a candidate motif, we will apply a paradigm that occurs throughout computational biology (and science in general) for determining whether an observation is significant. This approach asks how likely this observation would have been made in a *random* environment --- once again we see the power of randomness for answering practical questions.

For a classic example, many biologists are familiar with the search tool [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi), which allows researchers to compare a query (say, the DNA sequence of a newly sequenced gene) against a database to find whether the query appears with slight modifications in the database. Once BLAST finds a "hit" of the query in the database, it asks, "What are the chances we would find a hit of this quality in a random database?" If that probability is very low, then we can feel confident that the hit we found is significant.

**STOP:** How can we apply this paradigm to determine whether a transcription factor network contains a significant number of loops?

## Comparing a real transcription factor network against a random network

We will determine whether there are a significant number of loops in the transcription factor network of *E. coli* by comparing the number of loops that we find in the network against the expected number of loops we would find in a randomly generated network. If the number of loops in the real network is much higher than the number of loops in the random network, then we have strong evidence that there is some selective force causing a loop to be a network motif.

The next question is how to form a random network that offers a reasonable comparison against a real network.

## Forming a random network to compare against a transcription factor network

There are multiple ways to generate a random network, but we will use an approach developed by Edgar Gilbert in 1959. In this approach, we have are given an integer *n* and a probability *p* (between 0 and 1). We first form *n* nodes; then, for every possible pair of nodes *X* and *Y*, we have probability equal to *p* of connecting *X* to *Y* with a directed edge *X* → *Y*.

CITE:  Gilbert, E.N. (1959). "Random Graphs". Annals of Mathematical Statistics. 30 (4): 1141–1144. doi:10.1214/aoms/1177706098.

**STOP:** What should *n* and *p* be if we are generating a random network to compare against the *E. coli* transcription factor network?

* From Noah, needs to be integrated since we are using a subgraph of the E. coli network: "I used the TF-TF network from RegulonDB, so it's only transcription factors which interact with each other I believe (sorry, haven't added this as a citation yet). The library for viewing graphs wasn't able to handle larger networks, and I thought it looked more consistent to use the same graph viewer for both the random network and the ecoli network." What this means is that it could handle large networks but struggled to visualize them. So we should probably have the current ones but also mention how large the larger network is and give it to students if they want to play around with it.

In the spirit of making a fair comparison, we should therefore generate a random network with approximately the same number of nodes and edges. The *E. coli* transcription factor network has 197 nodes and 477 edges, so we will take *n* = 197. To ensure that the random network has approximately 477 edges, we first note that there are *n*<sup>2</sup> pairs of nodes that could have an edge connecting them (*n* choices for the starting node and *n* for the ending node). In order to ensure that we have approximately 477 edges in the random network, we set *p* equal to 477/*n*<sup>2</sup>.  On average, 477 of the number of pairs of nodes that will be selected for an edge is *n*<sup>2</sup>·(477/*n*<sup>2</sup>) = 477.

We are now ready to build a random network and compare the number of loops in this network with the number of loops in the real transcription factor network. If you'd like, the link below will take you to a short tutorial that includes a Jupyter notebook running this comparison that you can play around with yourself. If you'd rather skip ahead to the next section, we will give away that there a

[Visit tutorial](tutorial_loops){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


## Negative vs. positive autoregulation

* We can add more information to the TF network, labeling an edge *X* → *Y* with a "+" or "-" depending on whether the transcription factor *X* serves to increase or decrease the expression of *Y*.

* In a random network, we would expect about half of the edges to be assigned a "+", and about half of the edges to be assigned a "-".

* Re-examining the 130 total loops in the *E. coli* transcription factor network, we see that AAA of them are assigned a "+" and BBB of them are assigned a "-".

* This enormous discrepancy is doubtfully due to random chance; imagine if we flipped a coin 130 times and obtained AAA "heads" and BBB "tails".

* In other words, we have found that autoregulation is an important aspect of transcription factors, but we have also found that transcription factors that autoregulate tend to *negatively* autoregulate, meaning that they serve to *turn off* their own expression.

* This seems to have taken an even stranger turn --- why in the world would negative autoregulation be such a common phenomenon in transcription factors? In the next section, we will begin to unravel the mystery.

* Define: negative autoregulation

[Next lesson](nar){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
