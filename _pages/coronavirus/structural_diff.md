---
permalink: /coronavirus/structural_diff
title: "Structural and ACE2 Interaction Differences"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Jian Shang et. al. published a <a href="https://www.nature.com/articles/s41586-020-2179-y" target="_blank">paper</a> discussing the major structural differences between the the spike protein of SARS-CoV-2 and SARS-CoV. The focus is on the receptor-binding motif (RBM), which is the part of the receptor binding domain (RBD) of the spike protein that mediates contact with ACE2. The authors were able to locate three areas with significant differences that can provide clues as to why SARS-CoV-2 spike protein has greater affinity with ACE2 compared to SARS. Below is a brief summary on the differences, but reading the paper is highly recommended. In addition, we will use VMD to visualize the differences. For more in-depth description of how to visualize molecules, go to the <a href="https://purpleavatar.github.io/multiscale_biological_modeling/coronavirus/VMDTutorial">VMD Tutorial</a>.

#### Protein Structure Files

For their analysis, the authors purified and crystallized two protein complexes: SARS-CoV RBD complexed with ACE2 and chimeric SARS-CoV-2 RBD complexed with ACE2. The corresponding protein data bank entries are <a href="https://www.rcsb.org/structure/2AJF" target="_blank">2ajf</a> and <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a>, respectively.


#### Loop in ACE2-binding ridge

A marked difference was found on one of the loops in the ACE2-binding ridge. SARS-CoV contains a three residue motif, proline-proline-alanine, at residues 468 to 471. In contrast, SARS-CoV-2 contains a four residue motif, glycine-valine-glutamate-glycine, at the corresponding residues 482 to 485. The two bulky residues and two flexible glycines causes a conformational change in SARS-CoV-2 RBM with the following results:
* A main-chain hydrogen bond between Asn487 and Ala475 that creates a more compact ridge conformation, pushing the loop containing Ala475 to be closer to ACE2. This allows for the N-terminal residue Ser19 of ACE2 to form a hydrogen bond with the main chain of Ala475.
* Gln24 of the N-terminal helix of ACE2 forms a new contact with the RBM.
* Compared to the corresponding Leu472 of SARS-CoV, Phe486 of SARS-CoV-2 points in a different direction and is inserted into a hydrophobic pocket of Met82, Leu79, and Tyr83 in ACE2.

<img src="../_pages/coronavirus/files/Ridge.png">

The most noticeable difference is between SARS-CoV-2 Phe486 and SARS-CoV Leu472. In SARS-CoV-2, Phe486 (yellow) is points towards the hydrophobic pocket (silver). Due to phenylalanine's hydrophobic properties, this is a favorable interaction that may improve SARS-CoV-2 affinity with ACE2. In contrast, Leu472 (Yellow) in SARS-CoV does not appear to approach the hydrophobic pocket. 

#### Hotspot 31

In SARS-CoV RBM, Tyr442 supports the salt bridge between Lys31 and Glu35 of ACE2. However, the corresponding Leu455 residue in SARS-CoV-2 is less bulky and provides less support to Lys31 of ACE2. This causes the salt bridge to break, but allows Lys31 and Glu35 to form hydrogen bonds with Gln493 of SARS-CoV-2.

<img src="../_pages/coronavirus/files/Hotspot31.png">

This figure shows how the interaction between Lys31 and Glu35 (Red) of ACE2 changes drastically between SARS-CoV-2 and SARS-CoV. In SARS-CoV, the two residues appear to still be connected to each other through the salt bridge. On the other hand, the salt bridge does not appear to exist in SARS-CoV-2. Instead, the two residues point, almost in parallel, at Gln493 (blue) of SARS-CoV-2, possibly facilitating the formation of hydrogen bonds.

#### Hotspot 353

In SARS-CoV RBM, the methyl group of Thr487 supports the salt bridge between Lys353 and Asp38 of ACE2, and the side-chain hydroxyl group of Thr487 forms a hydrogen bond with the RBM main chain. The corresponding SARS-CoV-2 residue is Asn501 also forms a hydrogen bond between its side chain and RBM main chain. However, Asn501 provides less support to the salt bridge, causing Lys353 of ACE2 to be in a different conformation. Lys353 is then able to form a hydrogen bond with the main chain of SARS-CoV-2 RBM while maintaining the salt btidge with Asp38 of ACE2.

<img src="../_pages/coronavirus/files/Hotspot353.png">

The difference is much more subtle here than in the other two regions. Looking closely, it appears that Lys353 (left, red) of ACE2 is closer in proximity to the RBM in SARS-CoV-2 than in SARS-CoV, possibly allowing for hydrogen bond formation.

<hr>

To see how we made these visualizations, go to the following tutorial.

[Tutorial](tutorial_visualization){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

<hr>

[Next lesson](NAMD){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

