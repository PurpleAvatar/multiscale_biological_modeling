---
permalink: /coronavirus/structural_diff
title: "Structural and ACE2 Interaction Differences"
sidebar:
 nav: "coronavirus"
toc: true
toc_sticky: true
---

In part 1 of the module, we explored the different methods of predicting the 3D structure of a protein from its amino acid sequence, and how to assess the accuracy of our predicted structures. Because the protein's structure is critical to its function, we use protein structure prediction to analyze proteins where we have yet to determine its real structure using experimental techniques such as x-ray crystallography. Early SARS-CoV-2 researchers that wanted to study the S protein in January 2020 relied on structure prediction.

Now that research groups had enough time, the actual structure of the S protein have been determined and is available in the Protein Data Bank (PDB). With the structures, we can now producing the 3D visualizations the SARS-CoV-2 S protein and compare it with the SARS S protein to see if we can find some molecular explanation of why this virus is much more infectious than SARS.

## ACE2

In the [introduction](coronavirus_home), we discussed that SARS-CoV-2 and SARS both target the human angiotensin-converting enzyme 2 (ACE2) with their S protein. ACE2 is an enzyme that is present in most human organs and can be found on the surface of cells from various human tissues, including lung alveolar epithelial (outer layer) cells, small intestines eterocytes, arteries, and kidneys [^Hamming]. ACE2 is part of the renin-angiotensin system (RAS), which is critical in the regulation of the cardiovascular system and protective role of the lung alveolar epithelial cells [^Samavati]. 

This interaction of the S protein and ACE2 is an important step for the viral entry of both SARS-CoV-2 and SARS into the human cell. However, SARS-CoV-2 is much more infectious, and its S protein has been found to bind to ACE2 with greater affinity than that of SARS. The receptor binding domain (RBD) is the part of the S protein that interacts with ACE2, and the receptor binding motif (RBM) is the part of the RBD that mediates contact with ACE2. Therefore, we will narrow our focus to the differences in RBM to find out why SARS-CoV-2 binds better with ACE2.

* Add later: "All the analysis will be done using two software: ProDy and VMD. By the end of this module, you will be able to understand more about protein structure prediction and differences in the S proteins that attribute to the higher infectivity of COVID-19."

## Protein Structure Files
We will be using two PDB entries for comparison: <a href="https://www.rcsb.org/structure/2AJF" target="_blank">2ajf</a> and <a href="https://www.rcsb.org/structure/6vw1" target="_blank">6vw1</a>. 2ajf contains the structure of SARS RBD complexed with ACE2 and 6vw1 contains the structure of SARS-CoV-2 chimeric RBD complexed with ACE2. SARS-CoV-2 chimeric RBD consist of the SARS RBD core and SARS-CoV-2 RBM. The reason that the chimeric RBD was used is because the SARS RBD core helps facilitate crystallization by acting as the crystallization scaffold for X-ray diffraction (x-ray crystallography). Since the functional unit is still SARS-CoV-2 RBM, data from the comparisons should be similar or equivalent to using native SARS-CoV-2 RBD. Using these structures, we can produce 3D visualizations of SARS-CoV-2 RBD and SARS RBD interacting with ACE2 and see if we can determine structural differences between the interactions.

Here is a tutorial of how to use *Visual Molecular Dynamics* (VMD) to visualize the PDB entry 6vw1 showing the SARS-CoV-2 chimeric RBD complexed with ACE2.

[Visit tutorial](tutorial_visualization){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Three Sites of Conformational Differences
In the tutorial, we created the visualization of 6vw1 and highlighted specific amino acid residues in a region. This region is actually one of the places that differ greatly from the SARS RBD (2ajf). Jian Shang et. al., were able to identify three areas with significant conformational differences between the SARS-CoV-2 RBD and SARS RBD, each of which contributes to SARS-CoV-2 S protein’s increased affinity with ACE2 [^Shang].

### Loop in ACE2-binding ridge

A marked difference was found on one of the loops in the ACE2-binding ridge. This is the region that we visualized in the tutorial. SARS contains a three residue motif, proline-proline-alanine, at residues 468 to 471. In contrast, SARS-CoV-2 contains a four residue motif, glycine-valine-glutamate-glycine, at the corresponding residues 482 to 485. The two bulky residues and two flexible glycines causes a conformational change in SARS-CoV-2 RBM. Below is a visual comparison of this region between SARS-CoV-2 and SARS. See if you can spot the major difference before reading what actually happens. *Hint: Look at the yellow residue!*

<img src="../_pages/coronavirus/files/Ridge.png">

The most noticeable difference is between SARS-CoV-2 Phe486 and SARS Leu472. In SARS-CoV-2, Phe486 (yellow) is points towards the hydrophobic pocket (silver). Due to phenylalanine's hydrophobic properties, this is a favorable interaction that may improve SARS-CoV-2 affinity with ACE2. In contrast, Leu472 (Yellow) in SARS does not appear to approach the hydrophobic pocket. Here is a list of what the structural changes in SARS-CoV-2 result in:

* A main-chain hydrogen bond between Asn487 and Ala475 that creates a more compact ridge conformation, pushing the loop containing Ala475 to be closer to ACE2. This allows for the N-terminal residue Ser19 of ACE2 to form a hydrogen bond with the main chain of Ala475.
* Gln24 of the N-terminal helix of ACE2 forms a new contact with the RBM.
* Compared to the corresponding Leu472 of SARS, Phe486 of SARS-CoV-2 points in a different direction and is inserted into a hydrophobic pocket of Met82, Leu79, and Tyr83 in ACE2.

### Hotspot 31

Hotspot 31 is the second site of marked conformational differences between SARS-CoV-2 and SARS. Again, see if you can spot the differences, it should be more obvious this time around.

<img src="../_pages/coronavirus/files/Hotspot31.png">

This figure shows how the interaction between Lys31 and Glu35 (Red) of ACE2 changes drastically between SARS-CoV-2 and SARS. In SARS, the two residues appear to directly point towards each other. This is because in SARS RBM, Tyr442 supports the salt bridge between Lys31 and Glu35 of ACE2. In contrast to Tyr442 in SARS, the corresponding residue in SARS-CoV-2 is the less bulky Leu455, which provides less support to Lys31 of ACE2. This causes the salt bridge to break and results in Lys31 and Glu35 of ACE2 to point almost in parallel towards RBD residue Gln493. This change allows Lys31 and Glu35 to form hydrogen bonds with Gln493 in SARS-CoV-2.

### Hotspot 353

Finally, hotspot 353 is the third site of marked confromational differences between SARS-CoV-2 and SARS. Here, the difference between the residues is amazingly subtle, so much so that it takes a keen eye to even find them. See if you can find it.

<img src="../_pages/coronavirus/files/Hotspot353.png">

In SARS, the methyl group of Thr487 supports the salt bridge between Lys353 and Asp38 of ACE2, and the side-chain hydroxyl group of Thr487 forms a hydrogen bond with the RBM main chain. The corresponding SARS-CoV-2 residue Asn501 also forms a hydrogen bond between its side chain and RBM main chain. However, similar to what happened in hotspot 31, Asn501 provides less support to the salt bridge, causing Lys353 of ACE2 to be in a different conformation. Lys353 is then able to form an extra hydrogen bond with the main chain of SARS-CoV-2 RBM while maintaining the salt btidge with Asp38 of ACE2.

<hr>

We have identified three sites between SARS and SARS-CoV-2 when it comes to interacting with ACE2. Although we can see the differences visually, we still do not know how these differences actually contribute to SARS-CoV-2's increased affinity with ACE2. In the next section, we will try to quantitatively explain how these differences affect binding affinity with ACE2.

[Next lesson](NAMD){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^Hamming]: Hamming, I., Timens, W., Bulthuis, M., Lely, A., Navis, G., Goor, H. 2004. Tissue distribution of ACE2 portein, the functional receptor for SARS coronavirus. A first step in understanding SARS pathogenesis. J Pathol 203(2), 631-637. https://doi.org/10.1002/path.1570

[^Samavati]: Samavati, L., Uhal, B. 2020. ACE2, Much more than just a receptor for sars-cov-2. Front. Cell. Infect. Microbiol 10. https://doi.org/10.3389/fcimb.2020.00317 

[^Shang]: Shang, J., Ye, G., Shi, K., Wan, Y., Luo, C., Aijara, H., Geng, Q., Auerbach, A., Li, F. 2020. Structural basis of receptor recognition by SARS-CoV-2. Nature 581, 221–224. https://doi.org/10.1038/s41586-020-2179-y
