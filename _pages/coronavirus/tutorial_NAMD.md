---
permalink: /coronavirus/tutorial_NAMD
title: "VMD Plugin: NAMD Energy"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

This section will be on how to use NAMD Energy to calculate the interaction energy between SARS-CoV-2 RBD and ACE2. Be sure to have gone through *<a href="VMDTutorial" target="_blank">Setting up VMD</a>* on how to install VMD and load molecules into the program. In addition to VMD, make sure to download <a href="https://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=NAMD" target="_blank">NAMD</a>. One of the steps will require you to provide the path to *NAMD*.

First, load <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> into VMD. Afterwards, we will need to create a protein structure file (<a href="https://www.ks.uiuc.edu/Training/Tutorials/namd/namd-tutorial-unix-html/node23.html" target="_blank">PSF</a>) of 6vw1 in order to simulate the molecule. We will be using the VMD plugin *Atomatic PSF Builder* to create the file. From *VMD Main*, go to *Extensions>Modeling>Automatic PSF Builder*.

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

<hr>

<details>
 <summary>NAMD Energy Exercise 1</summary>
 Try to find the interaction energy between SARS-CoV-2 RBD loop site (residues 482 to 486) and ACE2. Use the chain pair B/F. Try to see if you can get the correct selection by yourself first. *Hint* the selection language is the very similar to that of VMD.
 <details>
  <summary>Selection Answer</summary>
 
  Selection 1: protein and chain B
  Selection 2: protein and chainF and (resid 482 to 486)
 </details>

 You should obtain values close to: Elect = -7.1162; vdW = -5.2101.
</details>

<details>
 <summary>NAMD Energy Exercise 2</summary>
 Try to find the interaction energy between SARS RBD and ACE2. Use the pdb file of <a href="https://www.rcsb.org/structure/2ajf" target="_blank">2ajf</a> and chain pair B/F for the selection step. You should obtain values close to: Elec = -130.517; vdW = -59.6941.
</details>

[Return to main text](NAMD){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
