---
permalink: /coronavirus/tutorial_multiseq
title: "VMD Plugin: Multiseq"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

In this tutorial, we will calculate Qres of the alignment of SARS-CoV-2 RBD and SARS RBD using the VMD plugin Multiseq and PDB entries of the RBDs: <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> and <a href="https://www.rcsb.org/structure/2ajf" target="_blank">2ajf</a>, respectively. Then, by locating regions of low Qres, we can identify regions of structural differences between the two.

Here, we will recreate the structural alignment analysis using *Qres* of SARS and SARS-CoV-2 RBD. Be sure to have installed VMD and know how to load molecules into the program. If you need a refresher, go to the <a href="tutorial_visualization" target="_blank">Visualization Tutorial</a>. The program may prompt you to download additional protein database information.

First, load <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> and <a href="https://www.rcsb.org/structure/2ajf" target="_blank">2ajf</a> into VMD. If you are unsure how to do this, follow the steps in the previous section titled *Loading Molecules*. Then, start up *Multiseq* by going to *Extensions>Analysis>Multiseq*.

<img src="../_pages/coronavirus/files/QresTutorial/Qres1.png">

You will see all the chains listed out per file. 

<img src="../_pages/coronavirus/files/QresTutorial/Qres2.png">

We only want to compare the RBD, so we will only keep chain F of each structure. To remove the other chains, click on the chain and go to *Edit>Cut*.

<img src="../_pages/coronavirus/files/QresTutorial/Qres3.png">

Go to *Tools>Stamp Structural Alignment* and a new window will open up. Keep all the values and click *OK*.

<img src="../_pages/coronavirus/files/QresTutorial/Qres4.png">
<img src="../_pages/coronavirus/files/QresTutorial/Qres5.png">

The structures are now aligned. To see coloring based on *Qres*, go to *View>Coloring>Qres*.

<img src="../_pages/coronavirus/files/QresTutorial/Qres6.png">

Blue indicates high *Qres* while blue indicates low *Qres*. *OpenGL Display* will now also reflect the color of *Qres* on the aligned structures. 

<img src="../_pages/coronavirus/files/QresTutorial/Qres7.png">

<img src="../_pages/coronavirus/files/QresTutorial/Qres8.png">

The color blue indicates residues with high Qres, indicated good structural alignment. The color red indicates residues with low Qres, meaning poor structural alignment. In your results, you should see regions of consecutive residues with low Qres. These are the regions where the two RBDs differ structurally.

<hr>

<details>
 <summary>Multiseq Exercise</summary>
 Try to perform structural alignment on SARS-CoV-2 Spike Chain A and SARS Spike Chain A. Use <a href="https://www.rcsb.org/structure/6vxx" target="_blank">6vxx</a> for SARS-CoV-2 and <a href="https://www.rcsb.org/structure/5xlr" target="_blank">5xlr</a> for SARS.
</details>

By finding regions of low Qres, we have identified where the RBDs differ structurally. Now, let's go back to the main text to see if our results are consistent with the three sites of marked conformational differences identified by Shang et. al.

[Return to main text](multiseq){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
