---
permalink: /coronavirus/VMDTutorial
title: "VMD Tutorial"
sidebar: 
 nav: "coronavirus"
---

This is a short tutorial on how to use VMD to visualize molecules and perform some basic analysis.

### Visualization

Here, we will recreate the VMD visualization of the ACE2-binding ridge of SARS-CoV-2 from the section <a href="https://purpleavatar.github.io/multiscale_biological_modeling/coronavirus/structural_diff" target="_blank">"Structural and ACE2 Interaction Differences"</a>

#### Loading Molecules

The first step is to download the protein structure of <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a> from the protein data bank. 

<img src="../_pages/coronavirus/files/Ridge%20Tutorial/Ridge0.png">

load the molecule into the program. In *VMD Main*, go to *File>New Molecule*. Click on *Browse*, select the molecule (.pdb) and click *Load*. The molecule should now be listed in *VMD Main* as well as the visualization in the *OpenGL Display*.

#### Moving Field of View

* In the *OpenGL Display* window, you can click and drag the molecule to change the orientation. Pressing ‘r’ on the keyboard allows you to rotate the molecule, pressing ‘t’ on the keyboard allows you to translate the molecule, and finally pressing ‘s’ allows you to enlarge or shrink the molecule.

#### Atom Selection, Drawing Method, and Coloring

* To change the visualization of the molecule or parts of the molecule, go to *Graphics>Representation*. Here, you can add, delete, or edit the visual representations. Double clicking on a representation will disable/enable it.

* *Selected Atoms* allows you to select specific parts of the molecule. The keyword “all” selects the entire molecule. To choose a specific chain, use the keyword “chain X”, where X is the chain of choice. To choose a specific residue, use the keyword “resid #”. Keywords can be combined using keywords “and” or ”or”, and more complicated selections need parenthesis. For example, “chain A or chain B” will select both chain A and B; “chain A and resid 3 to 10” will select residues 3 through 10 in chain A; “chain B and (resid 45 or 50)” will select residues 45 and 50 in chain B.

* *Coloring Method* allows you to change the coloring method of the selected atoms. This includes coloring based on element, amino acid residue, and many more. To choose a specific color, select *ColorID*.

* *Drawing Method* allows you to change the visualization of the selected atoms. *Tube* will focus only on the backbone of the molecule. *Cartoon/NewCartoon* will show secondary structure of the molecule (protein). *Licorice* will show the backbone and the sidechains of the molecule (protein).

### Analysis

#### Sequence Analysis

* To see the sequence of the molecule, in *VMD Main* go to *Extensions>Analysis>Sequence Viewer*. This will display the residues of the molecule.

* For sequence comparison, go to *Extensions>Analysis>MultiSeq*. Before comparing, delete any undesired molecules/chains. Next, go to *Tools>Sequence Alignment*, and click Ok. This will align the sequences. To see the differences using color, go to *View>Coloring>Sequence Identity*.

#### Structure Comparison

* To compare homologous structures, go to *Extensions>Analysis>MultiSeq* in *VMD Main*. Delete any undesired molecules/chains. Go to *Tools>Stamp Structural Alignment*. This will compare the structural differences between the selected molecules based on Qres. To see the differences using color, go to *View>Coloring>Qres*.

#### Normal Mode Wizard (NMwiz)

NMWiz is a plugin in VMD that is designed to be a GUI for ProDy. It uses ProDy for GNM, ANM, and PCA/EDA calculations, and then allows you to visualize the analysis within VMD.

* In *VMD Main*, go to *Extensions>Analysis>Normal Mode Wizard*. Then, choose *ProDy Interface*. This will allow you to choose which molecule and select which part of the molecule for analysis.

* ANM calculation will enable you to create animations of the molecule, displaying functional motions of the molecule. In addition, you can choose to see Crosscorrelation and Square-Fluctuation plots.

[Previous](rmsd_prody){: .btn .btn--primary .btn--x-large} [Next Page](#){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
