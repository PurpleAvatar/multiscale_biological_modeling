---
permalink: /coronavirus/multiseq
title: "Searching for Differences"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Shang et. al. provided a table comparing the critical ACE2-binding residues between different strains of coronavirus.

<img src="../_pages/coronavirus/files/ShangTable.png">

Imagine a scenario where we want to find regions of structural differences between SARS RBD and SARS-CoV-2 RBD, but the only data we have are the pdb files of *2ajf* and *6vw1*. A good starting point would be to use *<a href="https://www.ks.uiuc.edu/Research/vmd/plugins/multiseq/" target="_blank">Multiseq</a>*, a bioinformatics analysis environment that provides tools such as sequence and structural alignment. *Multiseq* is able to calculate structural conservation within aligned molecules using *Qres*.

<img src="../_pages/coronavirus/files/QresDef.png">

<img src="../_pages/coronavirus/files/QresResult.png">

The result showed four regions of structural differences, the main one being between SARS-CoV-2 residues 476 to 485. This coincides with the *Loop in ACE2-binding Ridge* that was identified by Shang et. al. Because *Multseq* is a VMD plugin, the *Qres* can be visualized on the structures. Below is the visualization of the imposed structures of SARS (*2ajf*) and SARS-CoV-2 (*6vw1*) RBD with ACE2 (in green). Blue represents regions of high *Qres* while red represents regions of low *Qres*. The highlighted region contains residues 476 to 485 of SARS-CoV-2, which includes the loop. It is important to note that this region is directly adjacent to SARS-CoV-2 Phe486 that is responsible for interacting with the ACE2 hydrophobic pocket.

<img src="../_pages/coronavirus/files/QresVMD.png">

To see how to use Multiseq and replicate these results, go to the following tutorial.

[Tutorial](tutorial_multiseq){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

<hr>

[Next lesson](NMA){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
