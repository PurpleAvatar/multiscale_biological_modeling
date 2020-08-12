---
permalink: /motifs/home
title: "Introduction: A Submicroscopic Scale of Interest"
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

In what follows, we will introduce yet another type of biological network involving the proteins that drive a cell's response to its environment. We will hunt for **network motifs**, or recurring structures hidden in a biological network. Furthermore, we will see how these motifs explain how a cell is able to make rapid, robust, and elegant responses in reaction to a changing environment.

But before we get ahead of ourselves, let us introduce some of the molecular biology fundamentals we will need to complete our analysis. As in the prologue, you may already have this biological background, in which case feel free to skim the next lesson.

[Next lesson](transcription){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
