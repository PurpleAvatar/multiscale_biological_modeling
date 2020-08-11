---
permalink: /motifs/transcription
title: "Transcription and Identifying DNA-Protein Binding"
sidebar:
 nav: "motifs"
---

### by Noah Lee and Phillip Compeau

In the [prologue](prologue), we worked with a particle-based model that simulated the interactions of skin cells to produce complex Turing patterns. In this module, we will zoom into a much lower biological scale and model the interactions between proteins and DNA.

DNA offers the lowest level of biological study: the DNA double helix is only about 2.5 nm across, and proteins may be on the order of about 10nm in diameter. To be clear about how tiny this is, a light microscope's highest resolution is about 200 times larger, and the barrier of what can be seen with the naked eye (say, the width of a human hair) is about 10,000 times larger.

This module will also introduce the concept of a **biological network**, an ubiquitous object in biological research that is highlighted in the figure below. When studying the interactions of proteins that may have similar function, biologists build a **protein-protein interaction network** in which nodes are proteins and two proteins are connected with an edge if they are known to interact. When examining the processes taking place within a cell, they form a **metabolic network**, in which nodes correspond to substances in the cell's chemical reactions, and an edge connects two nodes if there is some enzyme that catalyzes a reaction involving these two substances. Finally, neuroscientists study **neuronal networks** that link neurons together according to how they are linked in the nervous system --- these networks have been studied since the 1940s but have recently exploded as a model for solving applied problems in machine learning.

* NOAH: INSERT FIGURE WITH THREE EXAMPLES OF BIOLOGICAL NETWORKS
https://www.google.com/imgres?imgurl=https%3A%2F%2Fwww.researchgate.net%2Fprofile%2FErik_Verschueren%2Fpublication%2F271220492%2Ffigure%2Ffig2%2FAS%3A502973055934464%401496929529842%2FA-Complete-HCV-Host-Protein-Protein-Interaction-Network-in-Hepatoma-Cells-A-Network.png&imgrefurl=https%3A%2F%2Fwww.researchgate.net%2Ffigure%2FA-Complete-HCV-Host-Protein-Protein-Interaction-Network-in-Hepatoma-Cells-A-Network_fig2_271220492&tbnid=t1FQ3MWpxj3lGM&vet=12ahUKEwjtpYGDsY_rAhWBO98KHff8DXMQMygCegUIARC7AQ..i&docid=hhpPBG5vcrvUyM&w=850&h=508&q=protein-protein%20interaction%20network&ved=2ahUKEwjtpYGDsY_rAhWBO98KHff8DXMQMygCegUIARC7AQ
https://www.google.com/imgres?imgurl=https%3A%2F%2Fwww.researchgate.net%2Fprofile%2FChristine_Nazaret%2Fpublication%2F266399011%2Ffigure%2Ffig4%2FAS%3A272018578866176%401441865691027%2FThe-metabolic-network-of-tomato-cells-The-system-is-a-cell-with-symbolic-subcellular.png&imgrefurl=https%3A%2F%2Fwww.researchgate.net%2Ffigure%2FThe-metabolic-network-of-tomato-cells-The-system-is-a-cell-with-symbolic-subcellular_fig4_266399011&tbnid=pbMJPw0PjFAs0M&vet=12ahUKEwjH2KyKsY_rAhXWIN8KHd01DeIQMygCegUIARClAQ..i&docid=ukdQCOtCY8NjzM&w=427&h=566&q=cell%20metabolic%20network&ved=2ahUKEwjH2KyKsY_rAhXWIN8KHd01DeIQMygCegUIARClAQ
https://www.google.com/imgres?imgurl=https%3A%2F%2Fwww.researchgate.net%2Fprofile%2FHongyu_An4%2Fpublication%2F320567646%2Ffigure%2Ffig1%2FAS%3A656975884980224%401533646665749%2FNeuron-networks-a-brain-b-neural-network-c-neuron-connecting-structure-d-neuron.png&imgrefurl=https%3A%2F%2Fwww.researchgate.net%2Ffigure%2FNeuron-networks-a-brain-b-neural-network-c-neuron-connecting-structure-d-neuron_fig1_320567646&tbnid=T-KiR5l5WxguxM&vet=12ahUKEwiLi7ycsY_rAhUshuAKHcqvByMQMygEegUIARCrAQ..i&docid=cdB5bRVlM7gvYM&w=699&h=394&q=neuronal%20networks%20researchgate&ved=2ahUKEwiLi7ycsY_rAhUshuAKHcqvByMQMygEegUIARCrAQ

In what follows, we will introduce yet another type of biological network involving the proteins that drive a cell's response to its environment. By analyzing this network, we will be able to draw insights into how biological systems that lack any underlying intelligence can nevertheless evolve into structures that are powerful, even beautiful.

But before we get ahead of ourselves, let us introduce some of the molecular biology fundamentals we will need to complete our analysis. As in the prologue, you may already have this biological background, in which case feel free to skim the next section.

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
