---
permalink: /coronavirus/tutorial_multiseq
title: "VMD Plugin: Multiseq"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Here, we will recreate the structural alignment analysis using *Qres* of SARS and SARS-CoV-2 RBD. Be sure to have gone through *<a href="VMDTutorial" target="_blank">Setting up VMD</a>* on how to install VMD and load molecules into the program. The program may need to download additional protein database information.

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

<hr>

<details>
 <summary>Multiseq Exercise</summary>
 Try to perform structural alignment on SARS-CoV-2 Spike Chain A and SARS Spike Chain A. Use <a href="https://www.rcsb.org/structure/6vxx" target="_blank">6vxx</a> for SARS-CoV-2 and <a href="https://www.rcsb.org/structure/5xlr" target="_blank">5xlr</a> for SARS.
</details>

[Return to main text](multiseq){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
