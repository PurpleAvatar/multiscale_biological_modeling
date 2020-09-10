---
permalink: /motifs/transcription
title: "Transcription and Identifying DNA-Protein Binding"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Introduction to Transcription

Some of you might have heard about the [Central Dogma](https://www.youtube.com/watch?v=9kOGOY7vthk) and its power to convert genetic information in DNA (with base pairs A's, C's, T's, and G's) into useful proteins for the cell.

![image-center](../assets/images/Central_Dogma_of_Molecular_Biochemistry_with_Enzymes.jpg){: .align-center}
The "Central Dogma" of biology where DNA is transcribed into RNA which is translated into proteins[^dogma]
{: style="text-align: center;"}

[^book]: Compeau, P., & Pevzner, P. (2018). Bioinformatics Algorithms. La Jolla, CA: Active Learning.

From Bioinformatics Algorithms[^book],
"According to the Central Dogma, a gene from a genome is first transcribed into a strand of RNA composed of four ribonucleotides: adenine, guanine, cytosine, and uracil. A strand of RNA can be represented as an RNA string, formed over the four-letter alphabet {A, C, G, U}. You can think of the genome as a large cookbook, in which case the gene and its RNA transcript form a recipe in this cookbook. Then, the RNA transcript is translated into an amino acid sequence of a protein."

If you would like a refresher on transcription, the following video from the YouTube channel "*Professor Dave Explains*" will explain the process in eukaryotes at 1:09. For those more familiar with transcription, skip to 2:50, where Dave gives a great overview of why gene regulation is necessary.

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/J9jhg90A7Lw?start=69" frameborder="0" allowfullscreen></iframe>

As we saw in the video, regulation usually occurs on two targets: either the DNA which encodes a particular protein or the protein itself (both of which we will refer to as a "gene" in gene regulation). The proteins responsible for regulating the DNA to RNA process, the **transcription factors**, are crucial for allowing a cell to respond to external stimuli.

![image-center](../assets/images/signal_pathway.jpg){: .align-center}
A cell receiving a signal which triggers a response, resulting in transcription[^signalResponse]
{: style="text-align: center;"}

If a cell receives a signal from the environment, transcription factors are a crucial part of how the cell responds and acts on that signal. As we will later see in simple models, like Negative Autoregulation, the use of transcription factors not only enables a cell to respond to stimuli, but adjust the speed of the reaction as necessary. In more complicated models, like the Repressilator, proteins like transcription factors may rely on "*on*" or "*off*" states which are important for a cell to achieve just the right behavior.

## Determining if a given transcription factor regulates the expression of a given gene

A natural biological research question is to determine, for a given transcription factor, the collection of genes that this transcription factor regulates. A number of approaches have been used for this over the years, based on both computational and laboratory approaches.

For example, genes that are regulated by the same transcription factor often share the same "sequence motif", or a region of similarity that precedes the genes. Computational biologists have developed algorithms to scan through the genome, looking for regions of similarity that precede genes, and cluster genes based on these regions of similarity. If you are interested in learning more about these algorithms, we encourage you to check out [Chapter 2](https://www.bioinformaticsalgorithms.org/bioinformatics-chapter-2) of *Bioinformatics Algorithms: An Active Learning Approach*, which can be read for free online.

The current widespread practice for determining whether a protein bonds to a given region of DNA is called **ChIP-seq**[^chip], which stands for **chromatin immunoprecipitation sequencing**. This approach, which is illustrated in a figure below, combines an organism's DNA with a collection of proteins that bond to DNA (which in this case would be transcription factors). After allowing for the proteins to bond naturally to the DNA, the DNA (with proteins attached) is cleaved into much smaller fragments of a few hundred base pairs. As a result, we obtain a collection of DNA fragments, some of which are attached to a protein.

The question is how to isolate the fragments of DNA bonded to a single protein of interest. If we can do this for a transcription factor, then we will be able to infer the fragments of DNA to which that transcription factor binds.

The clever trick is to use an **antibody** (i.e., a protein that your immune system produces to identify foreign pathogens). The antibody is designed to bond to a single protein of interest, and it is attached to a bead so that once the antibody attaches to the protein target, we have a single complex consisting of the DNA fragment, the protein bonded to it, the antibody that recognized the protein, and the bead bonded to the antibody. Because of the bead, these complexes can be filtered out as "precipitate" from the solution, and we are left with just the DNA that bonds to the protein of interest.

In a final step, we unlink the protein from the DNA, so that we are left with a collection of DNA fragments that all bonded to the same transcription factor protein. These fragments are read using **DNA sequencing** to determine the order of nucleotides on each fragment. Once we have read the fragments, we can then scan the genome (an organism's sum total of DNA) to determine which genes the fragments precede. These must be the genes to which the given transcription factor binds!

![image-center](../assets/images/ChIP-seq_workflow.png){: .align-center}
<figcaption>An overview of ChIP-seq. Figure courtesy Jkwchui, Wikimedia Commons user.</figcaption>

If you are interested in a short lecture with a discussion of sequence motif finding and ChIP-seq, check out the following excellent video produced by students in the 2020 [PreCollege Program in Computational Biology](http://www.cbd.cmu.edu/education/pre-college-program-in-computational-biology/) at Carnegie Mellon. The presenters won an award from their peers for their work, and for good reason!

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/voEDurUgz_4" frameborder="0" allowfullscreen></iframe>

## Organizing transcription factor information

Researchers from around the world have contributed to determine which transcription factors regulate which genes for a variety of species, a task that is very much still ongoing. Our question is what we do with the huge amount of data that we obtain as a result of this research.

A natural question is how to organize the relationships between transcription factors and genes in a way that will help us identify patterns in these relationships. In the next section, we will borrow an idea introduced in the start of this module and see that a biological *network* will consolidate transcription factor information into a form that allows us to start to unlock the secrets of how cells have evolved to change the expression of genes quickly in response to a changing environment.

[Next lesson](networks){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^dogma]: CC BY-SA 3.0 https://creativecommons.org/licenses/by-sa/3.0/

[^signalResponse]: CC https://www.open.edu/openlearn/science-maths-technology/general-principles-cellular-communication/content-section-1

[^chip]: Johnson, D. S., Mortazavi, A., Myers, R. M., & Wold, B. (2007). Genome-wide mapping of in vivo protein-DNA interactions. Science, 316(5830), 1497–1502. https://doi.org/10.1126/science.1141319
