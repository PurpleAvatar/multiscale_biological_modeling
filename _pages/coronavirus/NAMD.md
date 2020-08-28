---
permalink: /coronavirus/tutorial_visualization
title: "Interaction Energy with ACE2"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

We identified and visualized three regions of marked conformational differences in the RBD of SARS Spike protein and SARS-CoV-2 Spike protein. However, how much do each region contribute to the binding of ACE2, and can we get a quantitative measure of how much the changes in the regions effect binding affinity? <a href="https://www.ks.uiuc.edu/Research/namd/" target="_blank">NAMD</a> is a parallel molecular dynamics code that was designed for high-performance large biomolecular system simulations that is most commonly used with VMD. <a href="https://www.ks.uiuc.edu/Research/vmd/plugins/namdenergy/" target="_blank">NAMD Energy</a> is a plugin within VMD that utilizes NAMD to evalute internal and interaction energies of molecules. This plugin will allow us to calculate the interaction energy between ACE2 and Spike RBD. In addition, NAMD Energy allows users to select specific regions, which will help us evaluate how much each of the three regions contributes.

*For protein-protein interactions, the key energies involved are electrostatic interactions (force from electric charge of atoms; Coulomb's Law) and van der Waals interactions (force from instantaneous and induced dipoles). Negative values indicate attractive force, and positive values indicate repulsion force. For NAMD, the standard unit for energy is kcal/mol.*

<img src="../_pages/coronavirus/files/NAMDEnergy.png">

*The .pdb files contain two biological assembies, or instances, of the corresponding structure. The first includes Chain A (ACE2) and Chain E (RBD), and the second includes Chain B (ACE2) and Chain F (RBD). The overall energy is calculated for both assemblies, while the following energies are only for the second assembly, Chain B and Chain F.*

From the results, we see that the overall attractive interaction energy between the RBD and ACE2 is higher for SARS-CoV-2, supporting the previous studies that found SARS-CoV-2 Spike having higher affinity with ACE2. For SARS-CoV-2, Hotspot31 (red) has the greatest contribution, followed by Hotspot353 (blue), and finally the loop in the RBM (yellow) providing the least. For SARS, Hotspot353 provides the greatest contribution, followed by the loop, and, surprisingly, Hotspot31 very slightly hindering the interaction. By comparing the results between SARS-CoV-2 and SARS, we can see that the residue differences and conformational changes in the three regions provides SARS-CoV-2 Spike protein with greater attractive interaction energy.

To see how to use NAMD Energy and replicate these results, go to the following tutorial.

[Tutorial](tutorial_NAMD){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

<hr>

[Next Lesson](multiseq){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

