---
permalink: /coronavirus/structural_diff
title: "Structural and ACE2 Interaction Differences"
sidebar: 
 nav: "coronavirus"
---
Jian Shang et. al. published a <a href="https://www.nature.com/articles/s41586-020-2179-y" target="_blank">paper</a> discussing the major structural differences between the the spike protein of SARS-CoV-2 and SARS-CoV. The focus is on the receptor binding domain (RBD) of the spike protein and its interaction with the human receptor ACE2. The authors were able to locate three areas with significant differences that can provide clues as to why SARS-CoV-2 spike protein has greater affinity with ACE2 compared to SARS. Below is a brief summary on the differences, but reading the paper is highly recommended. In the following pages, we will use VMD to visualize the differences described by the paper.

#### Loop in ACE2-binding ridge

A marked difference was found on one of the loops in the ACE2-binding ridge. SARS-CoV contains a three residue motif, proline-proline-alanine, at residues 468 to 471. In contrast, SARS-CoV-2 contains a four residue motif, glycine-valine-glutamate-glycine, at the corresponding residues 482 to 485. The two bulky residues and two flexible glycines causes a conformational change in SARS-CoV-2 RBD with the following results:
* A main-chain hydrogen bond between Asn487 and Ala475 that creates a more compact ridge conformation, pushing the loop containing Ala475 to be closer to ACE2. This allows for the N-terminal residue Ser19 of ACE2 to form a hydrogen bond with the main chain of Ala475.
* Gln24 of the N-terminal helix of ACE2 forms a new contact with the RBM.
* Compared to the corresponding Leu472 of SARS-CoV, Phe486 of SARS-CoV-2 points in a different direction and is inserted into a hydrophobic pocket of Met82, Leu79, and Tyr83 in ACE2.

#### Hotspot 31

In SARS-CoV RBD, Tyr442 supports the salt bridge between Lys31 and Glu35 of ACE2. However, the corresponding Leu455 residue in SARS-CoV-2 is less bulky and provides less support to Lys31 of ACE2. This causes the salt bridge to break, but allows Lys31 and Glu35 to form hydrogen bonds with Gln493 of SARS-CoV-2.

#### Hotspot 353

In SARS-CoV RBD, the methyl group of Thr487 supports the salt bridge between Lys353 and Asp38 of ACE2, and the side-chain hydroxyl group of Thr487 forms a hydrogen bond with the RBM main chain. The corresponding SARS-CoV-2 residue is Asn501 also forms a hydrogen bond between its side chain and RBD main chain. However, Asn501 provides less support to the salt bridge, causing Lys353 of ACE2 to be in a different conformation. Lys353 is then able to form a hydrogen bond with the main chain of SARS-CoV-2 RBD while maintaining the salt btidge with Asp38 of ACE2.

[Previous](rmsd2){: .btn .btn--primary .btn--x-large} [Next Page](#){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

