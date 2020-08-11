---
permalink: /motifs/transcription
title: "Transcription and Identifying DNA-Protein Binding"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Introduction to Transcription

* NOAH -- fill in this section. Would be great to have pictures and YouTube videos where needed as we don't want to reinvent the wheel when discussing transcription.

* Should have discussion of central dogma as well so that we can consider a "gene" to be either the DNA or the protein that it encodes. (This is important later.)

* Note to self: we don't have anything about the active form of a transcription factor. Technically it is this active form that we want to work with.

* Need to have an introduction to the biological process of transcription.  Disclaimer that learners with an in-depth knowledge of biology should skim it to the following section.

* As part of this discussion, mention how transcription factors serve as master regulators turning up or down the expression of a gene.

* These transcription factors are critical because they can help the cell respond to an external stimulus in which the transcription factor is activated by a chemical reaction taking place on the surface of the cell.  We will say more about this type of signal transduction process in a future chapter.

## Determining if a given transcription factor regulates the expression of a given gene

* Note: need to explain the experiment that can be used to determine whether or not *X* is a transcription factor for *Y*. (ChIP-seq). Also point toward [Chapter 2](https://www.bioinformaticsalgorithms.org/bioinformatics-chapter-2) of *Bioinformatics Algorithms: An Active Learning Approach*, which can be read for free online, for a deep dive in terms of how we can infer genes that are regulated by the same transcription factor.

* Also cite the following educational video produced by students in PreCollege 2020.

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/voEDurUgz_4" frameborder="0" allowfullscreen></iframe>

CITE first big ChIP-seq paper: https://science.sciencemag.org/content/316/5830/1497

## Transcription factor networks

Once we know which transcription factors regulate which genes, we will form a **transcription factor network** whose nodes are proteins and for which we connect *X* to *Y* with a directed edge if *X* is a transcription factor that regulates the expression of *Y*.  Note that according to this definition, any node can have an edge leading into it, but the only nodes with edges leaving them correspond to transcription factors.

The figure below shows a subset of the transcription factor network for *Escherichia coli*, the workhorse model organism of bacterial studies. *E. coli* is a simple organism, but we will still be able to draw powerful conclusions from studying its transcription factor network.

* NOAH: this is a very small image on my browser that is difficult to read -- can we make it larger or take a smaller subset of the network?

![image-center](../assets/images/motifs_finding_ecoli_1.jpeg){: .align-center}

**STOP:** Do you notice anything interesting about the *E. coli* transcription factor network?

Because of the size and complexity of the *E. coli* transcription factor network, we will need to analyze it computationally in order to draw rigorous conclusions about the structure of the network. However, the network does seem to have a large number of **loops**, or edges that connect a node to itself.

It is worth pausing for a moment to consider the implications of a loop in a transcription factor network. How can a transcription factor regulate itself?

A transcription factor is a protein, which means that by the Central Dogma, it is produced via transcription and translation of a gene appearing in an organism's DNA. It is therefore possible for a transcription factor to bind to the DNA upstream of the gene encoding the transcription factor, in a process called **autoregulation**. This type of  **feedback** is a beautiful feature of the biological system.

Yet we have two pressing questions. First, how can we argue rigorously that the number of loops in the transcription factor network for *E. coli* is significantly large? And second, if this is the case, then why is this feedback so common? In other words, why would a transcription factor have evolved to regulate its *own* transcription?

[Next lesson](finding){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
