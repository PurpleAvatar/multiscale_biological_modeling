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

A natural biological research question is to determine, for a given transcription factor, the collection of genes that this transcription factor regulates. A number of approaches have been used for this over the years, based on both computational and laboratory approaches.

For example, genes that are regulated by the same transcription factor often share the same "sequence motif", or a region of similarity that precedes the genes. Computational biologists have developed algorithms to scan through the genome, looking for regions of similarity that precede genes, and cluster genes based on these regions of similarity. If you are interested in learning more about these algorithms, we encourage you to check out [Chapter 2](https://www.bioinformaticsalgorithms.org/bioinformatics-chapter-2) of *Bioinformatics Algorithms: An Active Learning Approach*, which can be read for free online.

The current widespread practice for determining whether a protein bonds to a given region of DNA is called **ChIP-seq**, which stands for **chromatin immunoprecipitation sequencing**. This approach, which is illustrated in a figure below, combines an organism's DNA with a collection of proteins that bond to DNA (which in this case would be transcription factors). After allowing for the proteins to bond naturally to the DNA, the DNA (with proteins attached) is cleaved into much smaller fragments of a few hundred base pairs. As a result, we obtain a collection of DNA fragments, some of which are attached to a protein.

The question is how to isolate the fragments of DNA bonded to a single protein of interest. If we can do this for a transcription factor, then we will be able to infer the fragments of DNA to which that transcription factor binds.

The clever trick is to use an **antibody** (i.e., a protein that your immune system produces to identify foreign pathogens). The antibody is designed to bond to a single protein of interest, and it is attached to a bead so that once the antibody attaches to the protein target, we have a single complex consisting of the DNA fragment, the protein bonded to it, the antibody that recognized the protein, and the bead bonded to the antibody. Because of the bead, these complexes can be filtered out as "precipitate" from the solution, and we are left with just the DNA that bonds to the protein of interest.

In a final step, we unlink the protein from the DNA, so that we are left with a collection of DNA fragments that all bonded to the same transcription factor protein. These fragments are read using **DNA sequencing** to determine the order of nucleotides on each fragment. Once we have read the fragments, we can then scan the genome (an organism's sum total of DNA) to determine which genes the fragments precede. These must be the genes to which the given transcription factor binds!

![image-center](../assets/images/ChIP-seq_workflow.png){: .align-center}
<figcaption>An overview of ChIP-seq. Figure courtesy Jkwchui, Wikimedia Commons user.</figcaption>

If you are interested in a short lecture with a discussion of sequence motif finding and ChIP-seq, check out the following excellent video produced by students in the 2020 [PreCollege Program in Computational Biology](http://www.cbd.cmu.edu/education/pre-college-program-in-computational-biology/) at Carnegie Mellon. The presenters won an award from their peers for their work, and for good reason!

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/voEDurUgz_4" frameborder="0" allowfullscreen></iframe>

* NOAH: Please cite first big ChIP-seq paper when I introduce ChIP-seq: https://science.sciencemag.org/content/316/5830/1497

## Organizing data

* Transition from experiments to huge amount of data containing the relationship between transcription factors and the genes that they represent.

* Question is how to represent it.

* Transition to the next section.

[Next lesson](networks){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
