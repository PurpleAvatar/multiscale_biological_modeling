---
permalink: /coronavirus/home
title: "Module 3: Coronavirus"
sidebar:
 nav: "coronavirus"
---

### by Chris Lee and Phillip Compeau

### Introduction
Proteins are one of the most important groups of macromolecules in living organisms, contributing to essentially all functions within them. At the most basic level, proteins differ from each other by its amino acid sequence. However, it is how the amino acids fold into a three-dimensional structure and its dynamics that determines protein function. In fact, small perturbations in the structure can have a large impact on the protein’s functionality, even to the point of rendering the protein completely nonfunctional. Many experimental techniques, such as x-ray crystallography and mass spectrometry, have been developed that allows researchers to accurately determine protein structures. However, such  techniques have limitations, such as accessibility and costs. Fortunately, there are many publicly available softwares for protein structure prediction and protein analysis.

One of the most significant differences between the SARS (SARS-CoV 2003) and SARS-CoV-2 is their pathogenicity. While the two viruses belong to the same family of human coronavirus, there were only between 8-9 thousand SARS cases across 26 countries [^1]. On the other hand, the number of COVID-19 cases across the world continues to grow and has already surpassed 12 million across 216 countries or territories [^2]. Although there are many reasons attributed to this discrepancy, including governmental and political action, the biological differences between the two viruses also play a major role. Both coronaviruses have been found to recognize the human receptor ACE2, angiotensin-converting enzyme2 via the virus Spike protein, and it is this receptor recognition that facilitates the viral entry into human cells [^3],[^4]. More importantly, it has been found that the receptor binding domain (RBD) within the Spike protein of SARS-CoV-2 has greater affinity with ACE2 compared to SARS, which may contribute to why SARS-CoV-2 much more wide-spread.

This module will consist of two main sections. First, we will utilize three publicly available structure-prediction softwares to model the SARS-CoV-2 Spike protein and assess their accuracy using ProDy. Next, using ProDy and VMD, we will visualize and analyze the SARS-CoV-2 Spike protein and compare it with the SARS Spike protein.

### ProDy
<a href="http://prody.csb.pitt.edu/" target="_blank">ProDy</a> is an open-source Python package that allows users to perform protein structural dynamics analysis. Its flexibility allows users to select specific parts or atoms of the structure for conducting normal mode analysis and structure comparison.

### VMD
<a href="https://www.ks.uiuc.edu/Research/vmd/" target="_blank">VMD</a> (Visual Molecular Dynamics) is a program that is designed for modeling of molecules and macromolecules. Many plugins are available for in-depth analysis, including molecular dynamics simulations and interaction energy analysis. NMWiz (normal mode wizard), which was designed as a GUI for ProDy, is included within VMD, allowing for visualization of analysis using ProDy.

<hr>

The Spike protein is a trimer that is responsible for binding with human receptor ACE2. The RBD lies between residues 331 and 524 of the SARS-CoV-2 Spike protein, and is located at the "top" of the protein where it is highlighted in red in the second animation and the bottom image. 

<video width="320" height="240" controls>
<source type="video/mp4" src="../_pages/coronavirus/files/6vxxQSurf.mp4">
</video>


<video width="320" height="240" controls>
<source type="video/mp4" src="../_pages/coronavirus/files/6vxx.mp4">
</video>


<img src="../_pages/coronavirus/files/SpikeRBDTop.png">


[Protein Structure Prediction](prediction){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

##### Sources
[^1]: https://www.who.int/ith/diseases/sars/en/

[^2]: https://www.who.int/emergencies/diseases/novel-coronavirus-2019

[^3]: Shang, J., Ye G., Shi, K., Wan, Y., Luo, C., Aihara, H., Geng, Q., Auerbach, A., Li, F. Structural basis of receptor recognition by SARS-CoV-2. Nature 581, 221-224 (2020).

[^4]: Li, F., Li, W., Farzan, M., Harrison, S. C. Structure of SARS Coronavirus Spike Receptor-Binding Domain Complexed with Receptor. Science 309, 1864-1868 (2005).
