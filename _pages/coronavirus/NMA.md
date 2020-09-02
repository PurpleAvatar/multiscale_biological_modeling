---
permalink: /coronavirus/NMA
title: NMA Calculations
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---
## NMA Introduction

Proteins are not static, but rather dynamic structures. These fluctuations in their structures are typically key components their functions. Molecular dynamics (MD) is all about simulating molecules to analyze the movement of the molecules, atoms, and their interactions. However, simulating large structures, such as proteins with hundreds of amino acids, can prove to be extremely computationally heavy. Fortunately, there is an alternative method of studying large-scale movements of these structures called Normal mode analysis (NMA). NMA of proteins is based on the theory that the lowest frequency vibrational normal modes are the most functionally relavent, describing the largest movement within the protein.

One of the approaches for modeling a molecule is to represent atoms as nodes that are interconnected with springs, otherwise known as an elastic network model (ENM). The motivation of using ENM is that bonds actually share many characteristics with springs. We stated that proteins are not static, but this is true because the bonds that everythng together are not static either. Bonds are constantly vibrating, stretching and compressing much like that of a oscillating spring-mass system shown below. The bonded atoms are held together by sharing electrons, but is held at specific bond length due to the attraction and repulsion forces of the negatively charged electrons and positively charged nucleus. Just like a spring, when you bring the atoms closer together then the normal (equilibrium), they will resist with greater and greater repulsion force.

<div style='position:relative; padding-bottom:calc(309.00% + 44px)'><iframe src='https://gfycat.com/ifr/GaseousPoliticalAlaskajingle' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div>


Gaussian network model (GNM) is the ENM for isotropic fluctuations where only the fluctuation magnitudes are analyzed. Isotropic meaning that the physical properties don't change with direction. The anisotropic counterpart, where direction does matter, is called anisotropic network model (ANM), where the direction of the fluctuations are also considered. GNM and ANM are both popular methods for performing NMA.

One of the main strengths of ProDy is its capabilities for protein dynamics analysis. This includes performing both GNM and ANM analysis, allowing users to generate contact maps, cross-correlations, slow mode shape, and square fluctuations plots, all of which provide information on how the protein fluctuates. What these plots represent will be discussed below. VMD contains a plugin called Normal Mode Wizard (NMWiz), which is designed as a GUI for ProDy and allows users to perform ProDy's NMA directly in VMD. In addition, ANM calculations can also be visualized to produce animations of the protein.

For more information on NMA, GNM, and ANM, visit the following research articles:
* *<a href="https://www.sciencedirect.com/science/article/pii/S0166128008005435" target="_blank">Normal mode analysis for proteins</a>* by Lars Skjaerven et. al. (institutional access required)
* *<a href="https://www.pnas.org/content/106/30/12347" target="_blank">Protein elastic network models and the ranges of cooperativity</a>* by Lei Yang et. al.

## GNM Calculation of the Spike Protein

GNM Calculations were performed on SARS-CoV-2 Spike protein (<a href="http://www.rcsb.org/structure/6VXX" target="_blank">6vxx</a>) and SARS Spike protein (<a href="http://www.rcsb.org/structure/5xlr" target="_blank">5xlr</a>). Below are plots generated from the calculations. Perhaps unsurprisingly, the plots show very small differences between SARS-CoV-2 Spike and SARS spike proteins given that they are highly similar proteins in shape and function.

### Contact Map
{: .no_toc}

A protein contact map is a 2D matrix that represents the distance between all amino acid residues in the protein. In other words, it is essentially a reduced, 2D representation of a protein's tertiary structure. Contact map is another popular method of protein structure comparison. Proteins with very similar structures will have very similar contact map patterns, and deviations within the structure can be easily inferred by seeing unique patterns in only one of the proteins. Between all pairs of amino acids, the pair is assigned the value of 1 if the two residues are closer together than a predetermined threshold distance, and 0 otherwise. The threshold for the maps below is 20 Å, meaning that amino acid pairs within 20 Å of each other are assigned the value of 1.

<img src="../_pages/coronavirus/files/GNM/Contact.png">

### Cross-Correlation
{: .no_toc}

Protein residue cross-correlation shows the correlation between the fluctuations/displacement of residues. This graphical representation shows how the residues fluctuate relative to each other. The pair is assigned the value of 1 if the fluctuations are completely correlated, the value of -1 if the fluctuations are completely anticorrelated, and a value of 0 if uncorrelated. It is typical to see a diagonal of strong cross-correlation. Positive correlations coming off the diagonal represents correlations between contiguous residues and are characteristics of secondary structures. Common patterns for secondary structures are triangular structures for helices and plume structures for strands. Off-diagonal correlation and anticorrellations may potential represent interesting interactions between non-contiguous residues and domains.

<img src="../_pages/coronavirus/files/GNM/CrossCorr.png">

### Slow Mode Shape
{: .no_toc}

NMA is based on the idea that the lowest frequency modes describe the largest movement in the structure. Below is the plot of the lowest frequency (slowest) mode calculated by ProDy. Greater amplitudes represent regions of greater fluctuations. For example in the SARS-CoV-2 Chain A figure, we can see that the protein region between residues 200 and 500 fluctuate the most. The sign of the value represents relative direction of the fluctuation.

<img src="../_pages/coronavirus/files/GNM/SlowMode.png">

### Square Fluctuation
{: .no_toc}

This is another representation of the slowest mode with the same interpretation. Greater amplitudes represent regions of greater fluctuations.

<img src="../_pages/coronavirus/files/GNM/SqFlucts.png">

To see how to perform GNM calculations and create these maps and plots, go to the following tutorial.

[Visit tutorial](tutorial_GNM){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


## ANM Analysis and Animations Using NMWiz

NMWiz was designed as a GUI for ProDy and is available as a plugin for VMD. ANM calculations were performed using NMWiz on the SARS-CoV-2 Spike RBD (<a href="http://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a>) and SARS Spike RBD (<a href="http://www.rcsb.org/structure/2ajf" target="_blank">2ajf</a>). NMWiz is also able to generate cross-correlation and square fluctuation plots.

### Cross-Correlation
{: .no_toc}

<img src="../_pages/coronavirus/files/ANMImages/CrossCorr.png">

### Square Fluctuation
{: .no_toc}

<img src="../_pages/coronavirus/files/ANMImages/SqFlucts.png">

### Animations
{: .no_toc}

Because ANM also takes direction into consideration, it is possible to create animations of the protein fluctuation. The following animations are of the binding ridge between the Spike RBD (purple) and ACE2 (green). Important residues from regions of conformational differences between the two RBD (from the previous page) are also colored. 

*It is important to note that fluctuation calculated by ANM provides information on possible movement and flexibility, but does not depict actual protein movements.*

#### SARS-CoV-2 Spike Chimeric RBD (6vw1):
{: .no_toc}

<img src="../_pages/coronavirus/files/ANMImages/6vw1Legend.png"> <video width="640" height="480" controls><source type="video/mp4" src="../_pages/coronavirus/files/ANMImages/6vw1_B&F.mp4"></video>

#### SARS Spike RBD (2ajf):
{: .no_toc}

<img src="../_pages/coronavirus/files/ANMImages/2ajfLegend.png"> 
<video width="640" height="480" controls>
<source type="video/mp4" src="../_pages/coronavirus/files/ANMImages/2ajf_B&F.mp4">
</video>

<hr>

To see how to perform ANM calculations and animations, go to the following tutorial.

[Visit tutorial](tutorial_ANM){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

<hr>

[Next lesson](glycans){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
