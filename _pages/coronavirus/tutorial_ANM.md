---
permalink: /coronavirus/tutorial_ANM
title: "ANM Calculations & VMD Plugin: NMWiz"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Normal Mode Wizard (NMWiz) is a plugin in VMD that is designed to be a GUI for ProDy. It uses ProDy for normal mode analysis, including GNM and ANM calculations. In this section, we will perform ANM calculation and produce ANM animations of the SARS-CoV-2 Spike RBD. Be sure to have gone through *<a href="VMDTutorial" target="_blank">Setting up VMD</a>* on how to install VMD and load molecules into the program. 

First, load <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> into VMD by following the steps in the previous section *Loading Molecules*. Then, start up NMWiz by going to *Extensions>Analysis>Normal Mode Wizard*.

<img src="../_pages/coronavirus/files/ANMTutorial/Image1.png">

A small window will open. Select *ProDy Interface*

<img src="../_pages/coronavirus/files/ANMTutorial/Image2.png">

We want to focus only on the RBD of SARS-CoV-2, so we need to choose a new selection. In the *ProDy Interface*, change *Selection* to "protein and chain F" and click *Select*. Next, make sure that *ANM calculation* is selected for *ProDy job:*. Check the box for *write and load cross-correlations heatmap*. Finally click *Submit Job*.

<img src="../_pages/coronavirus/files/ANMTutorial/Image3.png">

*IMPORTANT*: Let the program run and do not click on any of the VMD windows as clicking on windows may cause the program to crash or become unresponsive. The job can take from a few seconds to a couple minutes. When the job is completed, you will see a new window *NMWiz - 6vw1_anm ...* and the cross=correlation heatmap appear.

<img src="../_pages/coronavirus/files/ANMTutorial/Image4.png">

<img src="../_pages/coronavirus/files/ANMTutorial/Image5.png">

Now that the ANM calculations are completed, you will see the visualization displayed in *VMD Main*. Disable the visualization of the original visualization of *6vw1* by double-clicking on the letter 'D'. The color red will represent that it is disabled.

<img src="../_pages/coronavirus/files/ANMTutorial/Image6.png">

In *OpenGL Display*, you will be able to see the protein with numerous arrows that represents the calculated fluctuations.

<img src="../_pages/coronavirus/files/ANMTutorial/Image7.png">

To actually see the protein move as described by the arrows, we have to create the animation. Go back to the *NMWiz - 6vw1_anm...* window and click *Make* next to *Animations*.

<img src="../_pages/coronavirus/files/ANMTutorial/Image8.png">

*VMD Main* should now display a new row for the animation.

<img src="../_pages/coronavirus/files/ANMTutorial/Image9.png">

The animation should also be visible in *OpenGL Display*. However, the previous visualizations are somewhat in the way. We can disable them in the same way as before by double-clicking on the letter 'D'.

<img src="../_pages/coronavirus/files/ANMTutorial/Image10.png">

Now, you should be able to clearly see the animation of the ANM fluctuations of 6vw1.

<video width="640" height="480" controls>
<source type="video/mp4" src="../_pages/coronavirus/files/ANMTutorial/6vw1_chainF.mp4">
</video>

<hr>

<details>
 <summary>ANM Animation Exercise</summary>
 Keeping the animation of the RBD, try to create the ANM animation of ACE2 (chain B). *This may take up to several minutes.* Once you finished, disable all visualizations except  for the animations in *VMD Main*. Go to *VMD>Representation* and make the following changes to the animations:

 <details>
  <summary>RBD Animation Representation</summary>
  <img src="../_pages/coronavirus/files/ANMTutorial/ANMExercise1.png">
 </details>

 <details>
  <summary>ACE2 Animation Representation</summary>
  <img src="../_pages/coronavirus/files/ANMTutorial/ANMExercise2.png">
 </details>


 Now, you should have fully recreated the animation from the *Normal Mode Analysis* page, showing the important residues from the identified three sites of differences between SARS-CoV-2 RBD and SARS RBD.

 <video width="640" height="480" controls><source type="video/mp4" src="../_pages/coronavirus/files/ANMImages/6vw1_B&F.mp4"></video>
</details>

[Return to main text](NMA){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

