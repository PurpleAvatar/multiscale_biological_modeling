---
permalink: /coronavirus/tutorial_visualization
title: "Visualizing Molecules"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Here, we will recreate the VMD visualization of the ACE2-binding ridge of SARS-CoV-2 from the section *<a href="https://purpleavatar.github.io/multiscale_biological_modeling/coronavirus/structural_diff" target="_blank">Structural and ACE2 Interaction Differences</a>*. Be sure to have gone through *<a href="VMDTutorial" target="_blank">Setting up VMD</a>* on how to install VMD and load molecules into the program. 

First, load 6vw1 into VMD. In the *OpenGL Display* window, you can click and drag the molecule to change the orientation. Pressing ‘r’ on the keyboard allows you to rotate the molecule, pressing ‘t’ on the keyboard allows you to translate the molecule, and finally pressing ‘s’ allows you to enlarge or shrink the molecule (or use scroll wheel). Note that left click and right click are different.

To change the visualization of the molecule or parts of the molecule, go to *Graphics>Representation*. 

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge4.png">

Here, you can add, delete, or edit the visual representations. Double clicking on a representation will disable/enable it. The file *6vw1.pdb* contains two biological assemblies of the structure. The first is made up of Chain A (ACE2) and Chain E (RBD), and the second is Chain B (ACE2) and Chain F (RBD). We will only focus on the second assembly. 

First, we will focus only on visualizing Chain B and excluding the rest. We will add in the other parts of the structure as we go.

* *Selected Atoms* allows you to select specific parts of the molecule. The keyword “all” selects all atoms in the file, so we will need to change it. Replace "all" with 'chain B'. Then, click on "Apply". *(In general, to choose a specific chain, use the keyword 'chain X', where X is the chain of choice. To choose a specific residue, use the keyword 'resid #'. Keywords can be combined using keywords “and” or ”or”, and more complicated selections need parenthesis.)*

* We will change the color of chain B to be green. *Coloring Method* allows you to change the coloring method of the selected atoms. This includes coloring based on element, amino acid residue, and many more. To choose a specific color, select *ColorID*. A drop-down list will appear to color selection. Choose "7" to select green.

* *Drawing Method* allows you to change the visualization of the selected atoms. "Lines" (also known as *wireframe*) simply draws a line between atoms to represent bonds. "Tube" will focus only on the backbone of the molecule. "Cartoon/NewCartoon" will show secondary structure of the molecule (protein). "Licorice" will show the backbone and the sidechains of the molecule (protein). We will choose "Tube" to only show the backbone of ACE2.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge5.png">

At this point, your *OpenGL Display* should look like this:

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge6.png">

Now, we will add in Chain F (SARS-CoV-2 chimeric RBD) and change the color to purple. Click on "Create Rep", which will duplicate the previous representation. Then, change *Selected Atoms* to "chain F" and *ColoringID* to "11" for purple. Make sure the choices are as follows:

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge7.png">

You should now see two distinct chains.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge8.png">

Finally, we will add in the specific residues (amino acids) of interest, which are Phe486, Ala475, and Asn487 of the RBD, and Met82, Leu79, Tyr83, Ser19, and Gln24 of ACE2. It is very similar to the previous steps of just adding new representations and changing *Selected Atoms*, *Coloring Method*, and *Drawing Method*. Make the following representations.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge9.png">

The final visualization should look like this:

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge10.png">

<details>
 <summary>Visualization Exercise</summary>
 Try to recreate the visualization of Hotspot31 for SARS-CoV-2 (same molecule as the tutorial). The important residues and their corresponding colors are listed on the left.

 <img src="../_pages/coronavirus/files/Hotspot31.png">
</details>

[Return to main text](structural_diff){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
