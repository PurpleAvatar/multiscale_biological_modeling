---
permalink: /motifs/networks
title: "Transcription Factor Networks"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Transcription factor networks

Once we know which transcription factors regulate which genes, we will consolidate this information into a bilogical network called a **transcription factor network**. The nodes in the network are an organism's proteins, and we connect *X* to *Y* with a directed edge if *X* is a transcription factor that regulates the expression of *Y*.  Note that any node can have an edge leading into it, but the only nodes with edges leaving them are transcription factors.

The figure below shows a subset of the transcription factor network for *Escherichia coli*, the workhorse model organism of bacterial studies. *E. coli* is a simple organism, but we will still be able to draw powerful conclusions from studying its transcription factor network.

* NOAH: this is a very small image on my browser that is difficult to read -- can we make it larger or take a smaller subset of the network?

![image-center](../assets/images/e_coli_tf_network_rotated.jpeg){: .align-center}

**STOP:** Do you notice anything interesting about the *E. coli* transcription factor network?
{: .notice--primary}

## Autoregulation

Because of the size and complexity of the *E. coli* transcription factor network, we will need to analyze it computationally in order to draw rigorous conclusions about the structure of the network. However, the network does seem to have a large number of **loops**, or edges that connect a node to itself.

It is worth pausing for a moment to consider the implications of a loop in a transcription factor network. How can a transcription factor regulate itself?

A transcription factor is a protein, which means that by the Central Dogma, it is produced via transcription and translation of a gene appearing in an organism's DNA. It is therefore possible for a transcription factor to bind to the DNA upstream of the gene encoding the transcription factor, in a process called **autoregulation**. This type of  **feedback** is a beautiful feature of the biological system.

Yet we have two pressing questions. First, how can we argue rigorously that the number of loops in the transcription factor network for *E. coli* is significantly large? And second, if this is the case, then why is this feedback so common? In other words, why would a transcription factor have evolved to regulate its *own* transcription?

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
