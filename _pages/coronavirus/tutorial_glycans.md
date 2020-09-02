---
permalink: /coronavirus/tutorial_glycans
title: "Glycan Counting"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Here, we will show how to visualize glycans in VMD. Be sure to have gone through *<a href="VMDTutorial" target="_blank">Setting up VMD</a>* on how to install VMD and load molecules into the program. 

First, load the open-state SARS-CoV-2 Spike, <a href="https://www.rcsb.org/structure/6VYB" target="_blank">6vyb</a> into VMD. For VMD, there is no specific keyword to select glycans. A workaround is to use the keywords: "not protein and not water". To recreate the basic VMD visualizations of the glycans in the module, use the following representations. (For the protein chains, use *Glass3* for *Material*).

<img src="../_pages/coronavirus/files/GlycanImage1.png">

The end result should look like this:

<img src="../_pages/coronavirus/files/GlycanImage2.png">

<hr>

<details>
 <summary>Visualization Exercise</summary>
 Try to recreate the visualization of Hotspot31 for SARS-CoV-2 (same molecule as the tutorial). The important residues and their corresponding colors are listed on the left.

 <img src="../_pages/coronavirus/files/Hotspot31.png">
</details>

[Return to main text](glycans){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
