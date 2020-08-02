---
permalink: /coronavirus/VMDTutorial
title: "VMD Tutorial"
sidebar: 
 nav: "coronavirus"
---

This is a short tutorial on how to use VMD to visualize molecules and perform some basic analysis. Before you start, make sure to have downloaded and installed <a href="https://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=VMD" target="_blank">VMD</a>.

### Visualization

Here, we will recreate the VMD visualization of the ACE2-binding ridge of SARS-CoV-2 from the section *<a href="https://purpleavatar.github.io/multiscale_biological_modeling/coronavirus/structural_diff" target="_blank">Structural and ACE2 Interaction Differences</a>*.

#### Loading Molecules

Download the protein structure of <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> from the protein data bank. 

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge0.png">

Next we can launch VMD and load the molecule into the program. In *VMD Main*, go to *File>New Molecule*. Click on *Browse*, select the molecule (6vw1.pdb) and click *Load*. 

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge1.png">
<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge2.png">

The molecule should now be listed in *VMD Main* as well as the visualization in the *OpenGL Display*.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge3.png">


#### Changing Graphical Representation: Atom/Residue Selection, Drawing Method, and Coloring

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

#### Moving Field of View

* In the *OpenGL Display* window, you can click and drag the molecule to change the orientation. Pressing ‘r’ on the keyboard allows you to rotate the molecule, pressing ‘t’ on the keyboard allows you to translate the molecule, and finally pressing ‘s’ allows you to enlarge or shrink the molecule (or use scroll wheel). Note that left click and right click are different.

### Analysis

#### Multiseq

Here, we will recreate the structural alignment analysis using *Qres* of SARS and SARS-CoV-2 RBD.

First, load <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> and <a href="https://www.rcsb.org/structure/2ajf" target="_blank">2ajf</a> onto VMD. If you are unsure how to do this, follow the steps in the previous section titled "Loading Molecules". Then, start up *Multiseq* by going to *Extensions>Analysis>Multiseq*.

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




#### Normal Mode Wizard (NMwiz)

NMWiz is a plugin in VMD that is designed to be a GUI for ProDy. It uses ProDy for GNM, ANM, and PCA/EDA calculations, and then allows you to visualize the analysis within VMD.

* In *VMD Main*, go to *Extensions>Analysis>Normal Mode Wizard*. Then, choose *ProDy Interface*. This will allow you to choose which molecule and select which part of the molecule for analysis.

* ANM calculation will enable you to create animations of the molecule, displaying functional motions of the molecule. In addition, you can choose to see Crosscorrelation and Square-Fluctuation plots.

[Previous](rmsd_prody){: .btn .btn--primary .btn--x-large} [Next Page](#){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
