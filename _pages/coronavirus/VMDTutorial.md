---
permalink: /coronavirus/VMDTutorial
title: "VMD Tutorial"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

This is a short tutorial on how to use VMD to visualize molecules and perform some basic analysis. Before you start, make sure to have downloaded and installed <a href="https://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=VMD" target="_blank">VMD</a>.

### Loading Molecules

These steps will be on how to load molecules into VMD. We will use the example of 6vw1.

Download the protein structure of <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> from the protein data bank. 

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge0.png">

Next we can launch VMD and load the molecule into the program. In *VMD Main*, go to *File>New Molecule*. Click on *Browse*, select the molecule (6vw1.pdb) and click *Load*. 

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge1.png">
<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge2.png">

The molecule should now be listed in *VMD Main* as well as the visualization in the *OpenGL Display*.

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge3.png">

<hr>

### Visualization: Changing Graphical Representations

Here, we will recreate the VMD visualization of the ACE2-binding ridge of SARS-CoV-2 from the section *<a href="https://purpleavatar.github.io/multiscale_biological_modeling/coronavirus/structural_diff" target="_blank">Structural and ACE2 Interaction Differences</a>*.

First, load 6vw1 into VMD be following the steps in *Loading Molecules*. In the *OpenGL Display* window, you can click and drag the molecule to change the orientation. Pressing ‘r’ on the keyboard allows you to rotate the molecule, pressing ‘t’ on the keyboard allows you to translate the molecule, and finally pressing ‘s’ allows you to enlarge or shrink the molecule (or use scroll wheel). Note that left click and right click are different.

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
 <summary>Exercise</summary>
 Try to recreate the visualization of Hotspot31.

 <img src="../_pages/coronavirus/files/Hotspot31.png">
</details>



<hr>

### NAMD Energy

This section will be on how to use NAMD Energy to calculate the interaction energy between SARS-CoV-2 RBD and ACE2. In addition to VMD, make sure to download <a href="https://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=NAMD" target="_blank">NAMD</a>. One of the steps will require you to provide the path to *NAMD*.

First, load <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> into VMD by following the steps in the previous section *Loading Molecules*. Afterwards, we will need to create a protein structure file (<a href="https://www.ks.uiuc.edu/Training/Tutorials/namd/namd-tutorial-unix-html/node23.html" target="_blank">PSF</a>) of 6vw1 in order to simulate the molecule. We will be using the VMD plugin *Atomatic PSF Builder* to create the file. From *VMD Main*, go to *Extensions>Modeling>Automatic PSF Builder*.

<img src="../_pages/coronavirus/files/NAMDTutorial/Image1.png">

In the *AutoPSF* window, make sure that the selected molecule is *6vw1.pdb* and the output to be *6vw1_autopsf*. Next click *Load input files*. In step 2, click *Protein* and then *Guess and split chains using current selections*. Afterwards, click *Create chains* and then *Apply patches and finish PSF/PDB*. 

<img src="../_pages/coronavirus/files/NAMDTutorial/Image2.png">

During this process, it is possible to see an error message stating "MOLECULE DESTROYED". If you see this message, click "Reset Autopsf" and repeat the steps again. The selected molecule will change, so make sure that the molecule is *6vw1.pdb* when you start over. Failed molecules remain in VMD, so deleting the failed molecule from *VMD Main* is recommended before each attempt.

<img src="../_pages/coronavirus/files/NAMDTutorial/Image3.png">

If the PSF file is successfully created, you will see a message stating "Structure complete." *VMD Main* also have an additional line.

<img src="../_pages/coronavirus/files/NAMDTutorial/Image4.png">

<img src="../_pages/coronavirus/files/NAMDTutorial/Image5.png">

Now that we have the PSF file, we can proceed to NAMD Energy. In *VMD Main*, go to *Extensions>Analysis>NAMD Energy*.

<img src="../_pages/coronavirus/files/NAMDTutorial/Image6.png">

The *NAMDEnergy* window will show up. First, change the molecule to be the PSF file. We want to calculate the interaction energy between the RBD and ACE2. Recall that the corresponding chain pairs are chain A (ACE2)/chain E (RBD) and chain B (ACE2)/chain F (RBD). Here we will use the chain B/F pair. Put "protein and chain B" and "protein and chain F" for *Selection 1* and *Selection 2*, respectively. Next, we want to calculate the main protein-protein interaction energies, electrostatic and van der Waals. Under *Output File*, enter in the desired name for the results. Next, we need to give NAMDEnergy the parameter file *par_all36_prot.prm*. This should be located at *VMD>plugins>noarch>tcl>readcharmmpar1.3>par_all36_prot.prm*. Finally, click *Run NAMDEnergy*.

<img src="../_pages/coronavirus/files/NAMDTutorial/Image7.png">

The output file will be created in your current working directory, and can be opened with a simple text-editor. The values of the results may vary very slightly upon repetitive calculations.

<img src="../_pages/coronavirus/files/NAMDTutorial/Image8.png">

{:: .notice--primary}
<details>
 <summary>Exercise 1</summary>
 Try to find the interaction energy between SARS-CoV-2 RBD loop site (residues 482 to 486) and ACE2. Use the chain pair B/F. Try to see if you can get the correct selection by yourself first. *Hint* the selection language is the very similar to that of VMD.
 <details>
  <summary>Selection Answer</summary>
 
  Selection 1: protein and chain B
  Selection 2: protein and chainF and (resid 482 to 486)
 </details>

 You should obtain values close to: Elect = -7.1162; vdW = -5.2101.
</details>

<details>
 <summary>Exercise 2</summary>
 Try to find the interaction energy between SARS RBD and ACE2. Use the pdb file of <a href="https://www.rcsb.org/structure/2ajf" target="_blank">2ajf</a> and chain pair B/F for the selection step. You should obtain values close to: Elec = -130.517; vdW = -59.6941.
</details>
<:/ .notice--primary}

<hr>

### Multiseq

Here, we will recreate the structural alignment analysis using *Qres* of SARS and SARS-CoV-2 RBD.

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

<details>
 <summary>Exercise</summary>
 Try to perform structural alignment on SARS-CoV-2 Spike Chain A and SARS Spike Chain A. Use <a href="https://www.rcsb.org/structure/6vxx" target="_blank">6vxx</a> for SARS-CoV-2 and <a href="https://www.rcsb.org/structure/5xlr" target="_blank">5xlr</a> for SARS.
</details>

<hr>

### NMWiz and ANM Animation

Normal Mode Wizard (NMWiz) is a plugin in VMD that is designed to be a GUI for ProDy. It uses ProDy for normal mode analysis, including GNM and ANM calculations. In this section, we will perform ANM calculation and produce ANM animations of the SARS-CoV-2 Spike RBD.

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

<details>
 <summary>Exercise</summary>
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


[Previous](prody){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
