---
permalink: /motifs/home
title: "Introduction to Transcription Factors"
sidebar:
 nav: "motifs"
---

### by Noah Lee and Phillip Compeau


## (Something about scale of interest)

* Discussion of the scale that we are interested in now -- a very fine-grained scale involving the interaction between proteins and genes.

* Biological networks and extending our particle simulators to answer questions about "why" and "how" unintelligent systems can build nontrivial systems.

## Introduction to transcription

* Need to have an introduction to the biological process of transcription.  Disclaimer that learners with an in-depth knowledge of biology should skim it to the following section.

* As part of this discussion, mention how transcription factors serve as master regulators turning up or down the expression of a gene.

* These transcription factors are critical because they can help the cell respond to an external stimulus in which the transcription factor is activated by a chemical reaction taking place on the surface of the cell.  We will say more about this type of signal transduction process in a future chapter.

# Determining if a given transcription factor regulates the expression of a given gene

* Note: need to explain the experiment that can be used to determine whether or not *X* is a transcription factor for *Y*. (ChIP-seq). Also point toward <a href="https://www.bioinformaticsalgorithms.org/bioinformatics-chapter-2" target="_blank">Chapter 2</a> of *Bioinformatics Algorithms: An Active Learning Approach*, which can be read for free online, for a deep dive in terms of how we can infer genes that are regulated by the same transcription factor.

CITE first big ChIP-seq paper: https://science.sciencemag.org/content/316/5830/1497

# Transcription factor networks

* Production of a network from transcription factors and proteins.  This will help us visualize relationships as well as look for patterns.

* Let's look at a subset of a TF network for *E. coli.*  This is just one example of a biological network.  (GIVE OTHERS: neural network, protein-protein interaction network)

* From Shuanger chapter: *Escherichia coli* (also *E. coli*) is a rod-shaped bacterium commonly found in the lower intestine of endotherms. Being commensal at the most of the time, it is, paradoxically, one of the main pathogens responsible for intraintestinal and extraintestinal infections.[^1] It is also the most widely studied prokaryotic model organism. (Need something about the fact that we share a lot with E. coli genetically.)

[^1] Tenaillon O, Skurnik D, Picard B, Denamur E. 2010. The population genetics of commensal *Escherichia coli*. Nature Reviews Microbiology 8:207-217. [Available online](https://www.nature.com/articles/nrmicro2298)

![image-center](../assets/images/motifs_finding_ecoli_1.jpeg){: .align-center}

* (WHAT ARE THE STATISTICS FOR THIS NETWORK)

* STOP: What do you see?

* What is clear is that we need some automated analysis of the network rather than relying on our own eyes due to the scale of the network.

* What our eyes do see is a lot of loops in which a transcription factor is connected to itself.

* There are two questions. One, is this anything out of the ordinary? And two, if that is true, why in the world would a transcription factor control its own regulation?

* In the next section, we will begin our analysis with a discussion of the first question.

## Separator

* Note to self: we don't have anything about the active form of a transcription factor. Technically it is this active form that we want to work with.

* Note: need to define "motif" somewhere.

[Click here to skip to the software tutorials](setup){: .btn .btn--primary}

## Learning objectives -- MOVE THESE

*Here are some learning motivators/outline of content*
1. What are motifs?
2. How does the common motif "negative autoregulation" work?
3. How can the motif "feed forward loop" change a cellular response?
4. How can a cell achieve oscillatory behaviors and how robust is this process?

[Next lesson](finding){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
