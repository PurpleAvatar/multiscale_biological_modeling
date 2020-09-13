---
permalink: /coronavirus/structural_diff
title: "Structural and ACE2 Interaction Differences"
sidebar:
 nav: "coronavirus"
toc: true
toc_sticky: true
---

## Need title

In the [introduction](coronavirus_home), we discussed that SARS-CoV-2 and SARS are in the same viral genus and both target the human angiotensin-converting enzyme2 (ACE2) with their S protein. However, SARS-CoV-2 is much more infectious, and its S protein has been found to bind to ACE2 with greater affinity than that of SARS. With accurate models of the tertiary structure of both S proteins, we can now structurally compare them to find why this is the case.
The receptor binding domain (RBD) is the part of the S protein that interacts with ACE2, and the receptor binding motif (RBM) is the part of the RBD that mediates contact with ACE2. Therefore, we will narrow our focus to the differences in RBM to find out why SARS-CoV-2 binds better with ACE2.

* Add later: "All the analysis will be done using two software: ProDy and VMD. By the end of this module, you will be able to understand more about protein structure prediction and differences in the S proteins that attribute to the higher infectivity of COVID-19."

## Protein Structure Files
We will be using two PDB entries for comparison: <a href="https://www.rcsb.org/structure/2AJF" target="_blank">2ajf</a> and <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a>. 2ajf contains the structure of SARS RBD complexed with ACE2 and 6vw1 contains the structure of SARS-CoV-2 chimeric RBD complexed with ACE2.
SARS-CoV-2 chimeric RBD consist of the SARS RBD core and SARS-CoV-2 RBM. The reason that the chimeric RBD was used is because the SARS RBD core helps facilitate crystallization by acting as the crystallization scaffold for X-ray diffraction (x-ray crystallography). Since the functional unit is still SARS-CoV-2 RBM, data from the comparisons should be similar or equivalent to using native SARS-CoV-2 RBD.

## Three Sites of Conformational Differences
Following a study by Jian Shang et. al., three areas with significant conformational differences were identified between the two structures which contributes to SARS-CoV-2 S protein’s increased affinity with ACE2 [^Shang]. Using *Visual Molecular Dynamics*, or VMD, we can visualize and see these differences.

### Loop in ACE2-binding ridge

A marked difference was found on one of the loops in the ACE2-binding ridge. SARS-CoV contains a three residue motif, proline-proline-alanine, at residues 468 to 471. In contrast, SARS-CoV-2 contains a four residue motif, glycine-valine-glutamate-glycine, at the corresponding residues 482 to 485. The two bulky residues and two flexible glycines causes a conformational change in SARS-CoV-2 RBM with the following results:
* A main-chain hydrogen bond between Asn487 and Ala475 that creates a more compact ridge conformation, pushing the loop containing Ala475 to be closer to ACE2. This allows for the N-terminal residue Ser19 of ACE2 to form a hydrogen bond with the main chain of Ala475.
* Gln24 of the N-terminal helix of ACE2 forms a new contact with the RBM.
* Compared to the corresponding Leu472 of SARS-CoV, Phe486 of SARS-CoV-2 points in a different direction and is inserted into a hydrophobic pocket of Met82, Leu79, and Tyr83 in ACE2.

<img src="../_pages/coronavirus/files/Ridge.png">

The most noticeable difference is between SARS-CoV-2 Phe486 and SARS-CoV Leu472. In SARS-CoV-2, Phe486 (yellow) is points towards the hydrophobic pocket (silver). Due to phenylalanine's hydrophobic properties, this is a favorable interaction that may improve SARS-CoV-2 affinity with ACE2. In contrast, Leu472 (Yellow) in SARS-CoV does not appear to approach the hydrophobic pocket.

### Hotspot 31

In SARS-CoV RBM, Tyr442 supports the salt bridge between Lys31 and Glu35 of ACE2. However, the corresponding Leu455 residue in SARS-CoV-2 is less bulky and provides less support to Lys31 of ACE2. This causes the salt bridge to break, but allows Lys31 and Glu35 to form hydrogen bonds with Gln493 of SARS-CoV-2.

<img src="../_pages/coronavirus/files/Hotspot31.png">

This figure shows how the interaction between Lys31 and Glu35 (Red) of ACE2 changes drastically between SARS-CoV-2 and SARS-CoV. In SARS-CoV, the two residues appear to still be connected to each other through the salt bridge. On the other hand, the salt bridge does not appear to exist in SARS-CoV-2. Instead, the two residues point, almost in parallel, at Gln493 (blue) of SARS-CoV-2, possibly facilitating the formation of hydrogen bonds.

### Hotspot 353

In SARS-CoV RBM, the methyl group of Thr487 supports the salt bridge between Lys353 and Asp38 of ACE2, and the side-chain hydroxyl group of Thr487 forms a hydrogen bond with the RBM main chain. The corresponding SARS-CoV-2 residue is Asn501 also forms a hydrogen bond between its side chain and RBM main chain. However, Asn501 provides less support to the salt bridge, causing Lys353 of ACE2 to be in a different conformation. Lys353 is then able to form a hydrogen bond with the main chain of SARS-CoV-2 RBM while maintaining the salt btidge with Asp38 of ACE2.

<img src="../_pages/coronavirus/files/Hotspot353.png">

The difference is much more subtle here than in the other two regions. Looking closely, it appears that Lys353 (left, red) of ACE2 is closer in proximity to the RBM in SARS-CoV-2 than in SARS-CoV, possibly allowing for hydrogen bond formation.

<hr>

To see how these visualizations were made, go to the following tutorial.

[Visit tutorial](tutorial_visualization){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

<hr>

In the next section, we will take a look at exactly how much these three differences in SARS-CoV-2 contribute to its increased affinity with ACE2.

[Next lesson](NAMD){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^Shang]: Shang, J., Ye, G., Shi, K., Wan, Y., Luo, C., Aijara, H., Geng, Q., Auerbach, A., Li, F. 2020. Structural basis of receptor recognition by SARS-CoV-2. Nature 581, 221–224. https://doi.org/10.1038/s41586-020-2179-y
