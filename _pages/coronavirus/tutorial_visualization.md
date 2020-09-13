---
permalink: /coronavirus/tutorial_visualization
title: "Visualizing Molecules"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

In this tutorial, we will go through how to visualize molecules in *Visual Molecular Dynamics* (VMD). Here we will visualize the PDB entry 6vw1, which contains the structure of the SARS-CoV-2 chimeric RBD complexed with ACE2. 

For this tutorial, please download VMD. The download can be found <a href="https://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=VMD" target="_blank">here</a>. 

We will need to download the PDB file for 6vw1. First follow this link to the PDB page for <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a>. Click on *Download Files* and select *PDB Format*.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge0.png">

Next, launch VMD. Three windows will open. *VMD.exe* is the console window, but we do not need to worry about it. *VMD Main* will be where we will be load molecules and change the visualizations. Finally, *OpenGL Display* will display the visualizations. Here, we want to load 6vw1 into VMD. In *VMD Main*, go to *File>New Molecule*. Click on *Browse*, select the molecule (6vw1.pdb) and click *Load*.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge1.png">
<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge2.png">

The molecule should now be listed in *VMD Main* as well as the visualization in the *OpenGL Display*.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge3.png">

In the *OpenGL Display* window, you can click and drag the molecule to change the orientation. Pressing ‘r’ on the keyboard allows you to rotate the molecule, pressing ‘t’ on the keyboard allows you to translate the molecule, and finally pressing ‘s’ allows you to enlarge or shrink the molecule (or use scroll wheel). Note that left click and right click are different.

To change the visualization of the molecule or parts of the molecule, go to *Graphics>Representation*. 

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge4.png">

Here, you can add, delete, or edit the visual representations. Double clicking on a representation will disable/enable it. The file *6vw1.pdb* contains two biological assemblies of the structure. The first is made up of Chain A (ACE2) and Chain E (RBD), and the second is Chain B (ACE2) and Chain F (RBD). We will only focus on the second assembly. 

First, we will focus only on visualizing Chain B and excluding the rest. We will add in the other parts of the structure as we go.

* *Selected Atoms* allows you to select specific parts of the molecule. The keyword “all” selects all atoms in the file, so we will need to change it. Replace "all" with 'chain B'. Then, click on *Apply*. *(In general, to choose a specific chain, use the keyword 'chain X', where X is the chain of choice. To choose a specific residue, use the keyword 'resid #'. Keywords can be combined using keywords “and” or ”or”, and more complicated selections need parenthesis.)*

* We will change the color of chain B to be green. *Coloring Method* allows you to change the coloring method of the selected atoms. This includes coloring based on element, amino acid residue, and many more. To choose a specific color, select *ColorID*. A drop-down list will appear to color selection. Choose "7" to select green.

* *Drawing Method* allows you to change the visualization of the selected atoms. "Lines" (also known as *wireframe*) simply draws a line between atoms to represent bonds. "Tube" will focus only on the backbone of the molecule. "Cartoon/NewCartoon" will show secondary structure of the molecule (protein). "Licorice" will show the backbone and the sidechains of the molecule (protein). We will choose "Tube" to only show the backbone of ACE2.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge5.png">

At this point, your *OpenGL Display* should look like this:

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge6.png">

Now, we will add in Chain F (SARS-CoV-2 chimeric RBD) and change the color to purple. Click on *Create Rep*, which will duplicate the previous representation. Then, change *Selected Atoms* to "chain F" and *ColoringID* to "11" for purple. Make sure the choices are as follows:

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge7.png">

You should now see two distinct structures based on color! (Remember that ACE2 is in green and the RBD is in purple.)

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge8.png">

We can also change the visualization to target specific residues (amino acids) within the structure. This is easily done by creating another representation and specifying the residue with the keyword "resid" followed by the residue number. Let's say that we were interested in residue 486 in the RBD. Click on *Create Rep*. In the new representation, change *Selected Atoms* to "chain F and resid 486" and click *Apply*. Then change the *Coloring Method* to "ColorID" and "4". Finally, change the *Drawing Method* to "Licorice".

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge8-1.png">

In *OpenGL Display*, you will now see a new yellow projection coming out of the RBD like the image below. This is residue 486! You may need to rotate the protein around to see it.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge8-2.png">

Now as an exercise, lets make representations for the following residues: Phe486, Ala475, and Asn487 of the RBD, and Met82, Leu79, Tyr83, Ser19, and Gln24 of ACE2. It is very similar to the previous steps of just adding new representations and changing *Selected Atoms*, *Coloring Method*, and *Drawing Method*. Make the following representations.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge9.png">

The final visualization should look like this:

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge10.png">

Congratulations! You have now create the visualizations of one of the three sites of major conformational differences between SARS-CoV-2 RBD and SARS RBD!

[Return to main text](structural_diff){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
