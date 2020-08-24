---
permalink: /coronavirus/accuracy
title: "Assessing Accuracy of Models"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

* Last section, we went two methods of protein structure prediction, *ab initio* and template-based (homology and threading), and how there are many competing groups with different approaches. Regardless of how the predicted models are created, we need a way to assess the accuracy of the software and algorithm. We can do this by predicting the structure of a protein already in the Protein Data Bank (PDB) and then comparing the predicted model with the experimentally determined structure

## Storing Protein Structure

* First, let’s see how protein structures are represented computationally. After experimentally determining the 3D protein structure, the structure is typically uploaded into the PDB as a .pdb file. This file is extremely dense as it holds all the details about the protein, from the very basic primary structure of the protein all the way to the position of every single atom. The simplest way to think about how the entire protein is stored is to first represent atoms as points on a 3D plane with each atom having its 3D orthogonal coordinates (X,Y,Z) in the unit of angstroms. This is the atomic coordinates of the protein. Because the structure of the 20 amino acids are well studied, we know which atoms are connected within each residue. The atomic bonds that link amino acids in sequence are easy to deduce from the primary structure of the protein. Connections between residues that cannot be deduced from the primary structure have to be specified (e.g. disulfide bonds). This is just scratching the tip of the iceberg of the information required to represent a protein structure. For more information, check out the <a href="http://www.wwpdb.org/documentation/file-format" target="_blank">official PDB documentation</a>.

<img src="../_pages/coronavirus/files/simplifiedPDB.png">

## RMSD

* One of the more popular methods of comparing the tertiary structure of proteins is Root Mean Square Deviation (RMSD). RMSD is used to quantitatively measure the difference between two paired sets of values. In simple terms, RMSD is calculated by square-rooting the sum of the squared difference between every pair. A lower RMSD value indicates a higher similarity between the two sets and a RMSD value of 0 indicates a perfect fit. Because of the way protein structures are stored, we can superpose two structures and easily use the atomic coordinates to calculate the RMSD between two structures given that they have the same number of atoms. The score would represent how much the positions of atoms deviate between the two structures, which is indicative of how different the overall structures are. By calculating RMSD between the protein model and the actual protein entry on PDB, we can assess how well the software and algorithm performed.

<img src="../_pages/coronavirus/files/RMSDExample.png">

* Due to the molecules being dynamic structures and constantly fluctuating, experimentally determined protein structures are not exact. In fact, most structures determined by x-ray crystallography, the most accurate method of structure determination, has a resolution between one to five angstroms. If we were to compare every single atom between two structures, the RMSD score can be greatly inflated Therefore, we typically only use the minimum requirement and compare the positions of the alpha-Carbons of the protein backbone. Just from the positions of the alpha-Carbons, we can get a pretty good idea of the tertiary structure of the protein (refer back to <a href="structure_intro">Introduction to Protein Structure Prediction</a>).

*	Unfortunately, there is no established threshold RMSD as scores vary based on protein size (larger proteins mean more fluctuating parts) and the resolution of the structure determination method. In addition, RMSD has its own flaws where a single misplaced loop or an off-angle bond can have profound effects on the score. This is why other methods of structure comparisons are used in conjunction to RMSD for a more thorough comparison analysis. Nonetheless, a score under 2.0 angstroms is typically acceptable when comparing large molecules such as proteins.

<img src="../_pages/coronavirus/files/RMSDExample2.png">

If you want to learn more about RMSD and how to do your own calculations or are curious on how well our own SARS-CoV-2 models performed, visit the following tutorial.

[Tutorial](rmsd2){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

## Other Accuracy Accessing Methods (if needed)

<hr>

[Next lesson](structural_diff){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}