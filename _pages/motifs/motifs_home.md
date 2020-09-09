---
permalink: /motifs/home
title: "Introduction: A Submicroscopic Scale of Interest"
sidebar:
 nav: "motifs"
---

### by Noah Lee and Phillip Compeau

In the [prologue](prologue), we worked with a particle-based model that simulated the interactions of skin cells to produce complex Turing patterns. In this module, we will zoom into a much lower biological scale and model protein interactions, which occur on a molecular level.

DNA offers the lowest level of biological study: the DNA double helix is only about 2.5 nm across, and proteins may be on the order of about 10nm in diameter. To be clear about how tiny this is, a light microscope's highest resolution is about 200 times larger, and the barrier of what can be seen with the naked eye (say, the width of a human hair) is about 10,000 times larger.

This module will also introduce the concept of a **biological network**, a ubiquitous object in biological research that is highlighted in the figure below. When studying the functions and binding of proteins, biologists may build a **protein-protein interaction network** in which nodes are proteins and two proteins are connected with an edge if they are known to interact. When examining the more complex interactions and processes taking place within a cell, they form a **metabolic network**. Here, nodes correspond to any substances in a chemical reactions and an edge connects two nodes if there is some enzyme that catalyzes a reaction involving these substances. Finally, neuroscientists study **neuronal networks** that link neurons together according to how they are linked in the nervous system --- these networks have been studied since the 1940s but have recently exploded as a model for solving applied problems in machine learning.

![image-center](../assets/images/A-Complete-HCV-Host-Protein-Protein-Interaction-Network-in-Hepatoma-Cells-A-Network.png){: .align-center}
A Complete HCV-Host Protein-Protein Interaction Network in Hepatoma Cells[^PPInetwork]
{: style="text-align: center;"}

![image-center](../assets/images/The-metabolic-network-of-tomato-cells-The-system-is-a-cell-with-symbolic-subcellular.png){: .align-center}
The metabolic network of tomato cells[^metabolicNetwork]
{: style="text-align: center;"}

![image-center](../assets/images/Neuron-networks-a-brain-b-neural-network-c-neuron-connecting-structure-d-neuron.png){: .align-center}
Mapping and models of neurons[^neuralNetwork]
{: style="text-align: center;"}

In what follows, we will introduce yet another type of biological network involving the proteins that drive a cell's response to its environment. We will hunt for **network motifs**, or recurring structures hidden in a biological network. Furthermore, we will see how these motifs explain how a cell is able to make rapid, robust, and elegant responses in reaction to a changing environment.

But before we get ahead of ourselves, let us introduce some of the molecular biology fundamentals we will need to complete our analysis. As in the prologue, you may already have this biological background, in which case feel free to skim the next lesson.

[Next lesson](transcription){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^neuralNetwork]: An, Hongyu. (2017). Opportunities and challenges on nanoscale 3D neuromorphic computing system. 10.1109/ISEMC.2017.8077906.
[^metabolicNetwork]: Colombie, Sophie & Nazaret, Christine & Bénard, Camille & Biais, Benoit & Mengin, Virginie & Solé, Marion & Fouillen, Laetitia & Dieuaide‐Noubhani, Martine & Mazat, Jean-Pierre & Beauvoit, Bertrand & Gibon, Yves. (2014). Modelling central metabolic fluxes by constraint-based optimization reveals metabolic reprogramming of developing Solanum lycopersicum (tomato) fruit. The Plant Journal. 81. 10.1111/tpj.12685.
[^PPInetwork]: Ramage, Holly & Kumar, Gagandeep & Verschueren, Erik & Johnson, Jeffrey & Dollen, John & Johnson, Tasha & Newton, Billy & Shah, Priya & Horner, Julie & Krogan, Nevan & Ott, Melanie. (2015). A Combined Proteomics/Genomics Approach Links Hepatitis C Virus Infection with Nonsense-Mediated mRNA Decay. Molecular cell. 57. 329-340. 10.1016/j.molcel.2014.12.028
