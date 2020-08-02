---
permalink: /motifs/home
title: "Introduction to Transcription Factors"
sidebar:
 nav: "motifs"
---

### by Noah Lee and Phillip Compeau


## A new scale of interest

In the [Prologue](prologue), we worked with a particle-based model that could be thought of as simulating the interactions of cells in the skin of zebrafish. In this module, we will look at a much lower biological scale and model the interactions between proteins and DNA. This is in a sense the lowest level of biological study: the DNA double helix is only about 2.5 nm across, and proteins may be on the order of about 10nm in diameter. To be clear about how tiny this is, the smallest object that a light microscope can pick out is about 500 nm. For comparison, the width of a single human hair --- at the barrier of what can be seen with the naked eye --- is typically about 200 times larger.

This chapter will also introduce the concept of a **biological network**, which are ubiquitous in biological research. When studying interactions of proteins that may have similar function, biologists build a **protein-protein interaction network** in which nodes are proteins and two proteins are connected with an edge if they are known to interact. When examining the processes taking place within a cell, they form a **metabolic network** in which nodes correspond to substances in the cell's chemical reactions and an edge connects two nodes if there is some enzyme that catalyzes a reaction involving these two substances. Finally, neuroscientists study **neuronal networks** that link neurons together according to how they are linked in the nervous system --- these networks have been studied since the 1940s but have recently exploded as a model that can be used to solve problems in machine learning.

NOAH: INSERT FIGURE WITH THREE EXAMPLES OF BIOLOGICAL NETWORKS

In what follows, we will introduce yet another type of biological network involving the proteins that drive a cell's response to its environment. By analyzing this network, we will be able to draw insights into how biological systems that lack any underlying intelligence can nevertheless evolve into structures that are powerful, even beautiful.

But before we get ahead of ourselves, let us introduce some of the molecular biology fundamentals we will need to complete our analysis. As in the Prologue, you may already have this biological background, in which case feel free to skim the next section.

## Introduction to transcription

* NOAH -- fill in this section. Would be great to have pictures and YouTube videos where needed as we don't want to reinvent the wheel when discussing transcription.

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
