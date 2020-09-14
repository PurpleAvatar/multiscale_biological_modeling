---
permalink: /coronavirus/multiseq
title: "Searching for Differences"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Imagine a scenario where we want to find regions of structural differences between SARS RBD and SARS-CoV-2 RBD, but the only data we have are their 3D structures from the PDB: *2ajf* for SARS RBD and *6vw1* for SARS-CoV2. Based on what we saw in the previous lesson, the differences can be extremely subtle and takes a keen eye to even find them. Fortunately, there are tools that can help us identify where the two structures deviate from each other. A good starting point would be to use *<a href="https://www.ks.uiuc.edu/Research/vmd/plugins/multiseq/" target="_blank">Multiseq</a>*, a bioinformatics analysis environment that provides tools such as sequence and structural alignment. *Multiseq* is able to calculate structural conservation within aligned molecules by computing Q per residue. **Q** is a parameter that is used to indicate structural identity (how similar the structures are), and is similar to RMSD in that it depends on the distance between alpha carbons. Below is the equation for Q [^Eastwood].

<a href="https://www.codecogs.com/eqnedit.php?latex=Q&space;=&space;\frac{2}{(N-1)(N-2)}\sum_{i<j-1}exp[-\frac{(r_{ij}-r_{i,j}^N)^2}{2\sigma_{ij}^2}]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Q&space;=&space;\frac{2}{(N-1)(N-2)}\sum_{i<j-1}exp[-\frac{(r_{ij}-r_{i,j}^N)^2}{2\sigma_{ij}^2}]" title="Q = \frac{2}{(N-1)(N-2)}\sum_{i<j-1}exp[-\frac{(r_{ij}-r_{i,j}^N)^2}{2\sigma_{ij}^2}]" /></a>

where: 
 * N = number of residues
 * $$r_{ij}$$ = distance between alpha carbon pair
 * $$r_{ij}^N$$ = alpha carbon distance between residue i and residue j in the protein native state
 * $$\sigma_{ij}^2$$ = standard deviation
 * $$0 < Q \leq 1$$

Q = 1 indicates that the aligned structures are identical. A low Q score implies that the structures do not align well and are different.
 
**Q per residue (Qres)** is the measure of contribution of each residue to the overall Q value of the aligned structures. This is very useful for finding specific regions where the aligned proteins differ structurally from each other. To find these regions, we just need to locate regions where many residues have low Qres.

<hr>

In this tutorial, we will use Multiseq to align the SARS-CoV-2 (chimeric) RBD and SARS RBD using the PDB entries <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> and <a href="https://www.rcsb.org/structure/2AJF" target="_blank">2ajf</a>, respectively. Then, we will locate areas of structural differences be computing Qres.

[Visit tutorial](tutorial_multiseq){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

<hr>

In the tutorial, we calculated Qres between SARS-CoV-2 RBD and SARS RBD and identified four regions of structural differences, the main one being between SARS-CoV-2 residues 476 to 485 shown below.

<img src="../_pages/coronavirus/files/QresResult.png">

Shang et. al. had identified three sites of marked conformational differences between the two RBD and provided a table comparing the critical ACE2-binding residues between different strains of coronavirus.

<img src="../_pages/coronavirus/files/ShangTable.png"> 

One of the regions from this table overlaps with the region we identified using Qres. This region is the *Loop in ACE2-binding Ridge*, one of the three sites. This means that computing and analyzing Qres is a valid method of searching for areas of structural differences. However, it was not able to capture all three of the sites, perhaps due to how subtle the differences can be. As such, we may need to employ other tools to find all areas of structural differences.
 
Because *Multseq* is a VMD plugin, the *Qres* can be visualized on the structures. Below is the visualization of the imposed structures of SARS (*2ajf*) and SARS-CoV-2 (*6vw1*) RBD with ACE2 (in green). Blue represents regions of high *Qres* while red represents regions of low *Qres*. The highlighted region contains residues 476 to 485 of SARS-CoV-2, which includes the loop. It is important to note that this region is directly adjacent to SARS-CoV-2 Phe486 that is responsible for interacting with the ACE2 hydrophobic pocket.

<img src="../_pages/coronavirus/files/QresVMD2.png">

In the next lesson, we will discuss another method of analyzing and comparing protein structures that uses molecular dynamics.

[Next lesson](NMA){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^Eastwood]: Eastwood, M. P., Hardin, C., Luthey-Schulten, Z., Wolynes, P. G. 2001. Evaluating protein structure-prediction schemes using energy landscape theory. IBM Journal of Research and Development 45(3.4), 475-497. https://doi.org/10.1147/rd.453.0475
