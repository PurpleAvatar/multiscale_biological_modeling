---
permalink: /motifs/networks
title: "Transcription Factor Networks"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Transcription factor networks

Once we know which transcription factors regulate which genes, we will consolidate this information into a bilogical network called a **transcription factor network**. The nodes in the network are an organism's proteins, and we connect *X* to *Y* with an edge if *X* is a transcription factor that regulates the expression of *Y*.  Note that any node can have an edge leading into it, but the only nodes with edges leaving them are transcription factors.

![image-center](../assets/images/s_cerevisiae_tf_network.jpg){: .align-center}
Example of different motifs within the *S. Cerevisiae* network[^scNetwork]
{: style="text-align: center;"}

The figure below shows a subset of the transcription factor network for *Escherichia coli*, the workhorse model organism of bacterial studies. *E. coli* is a simple organism, but we will still be able to draw powerful conclusions by studying its transcription factor network.

![image-center](../assets/images/e_coli_tf_network.jpeg){: .align-center}
To view this network in more detail you can download <a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/e_coli_tf_network.jpeg" download="e_coli_tf_network.jpeg">here</a>, or to see the full *e. coli* network, see [here](https://bmcsystbiol.biomedcentral.com/articles/10.1186/1752-0509-2-21)

**STOP:** Do you notice anything interesting about the *E. coli* transcription factor network?
{: .notice--primary}

Note also that the edges in the *E. coli* transcription factor network are colored red or green. An edge connecting *X* to *Y* is colored green if *X* upregulates *Y*, and it is colored red if *X* downregulates *Y*. (Alternatively, we could label the edges with a "+" or "-", respectively.)

**STOP:** How to you think that researchers measure whether a transcription factor upregulates or downregulates a given gene?
{: .notice--primary}

## Autoregulation

Because of the size and complexity of the *E. coli* transcription factor network, we will need to analyze it computationally to draw rigorous conclusions about the network's structure. However, we do note that the network does seem to have a large number of **loops**, or edges that connect a node to itself.

It is worth pausing for a moment to consider the implications of a loop in a transcription factor network. What does it even mean for a transcription factor regulate itself?

A transcription factor is a protein, which means that by the Central Dogma of Molecular Biology, the transcription factor is produced as the result of transcription and then translation of a gene appearing in an organism's DNA. In a process called **autoregulation**, the transcription factor protein then binds to the DNA in the upstream region of the gene encoding the *same* transcription factor. This type of **feedback** is a beautiful feature of this biological system.

![image-center](../assets/images/autoregulation_example.png){: .align-center}
The autoregulation process[^auto]
{: style="text-align: center;"}

The presence of transcription factor autoregulation leads us to ask two questions. First, how can we show that the number of loops in the transcription factor network for *E. coli* is significantly large? And second, if this is the case, then why is autoregulation common? Put another way, why would a transcription factor have evolved to regulate its *own* transcription?


[Next lesson](nar){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


[^scNetowrk]: Lee, T. I., Rinaldi, N. J., Robert, F., Odom, D. T., Bar-Joseph, Z., Gerber, G. K., … Young, R. A. (2002). Transcriptional regulatory networks in Saccharomyces cerevisiae. Science, 298(5594), 799–804. https://doi.org/10.1126/science.1075090
[^auto]: Arani, B. M. S., Mahmoudi, M., Lahti, L., González, J., & Wit, E. C. (2018). Stability estimation of autoregulated genes under Michaelis-Menten-type kinetics. Physical Review E, 97, 62407. https://doi.org/10.1103/PhysRevE.97.062407