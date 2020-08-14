---
permalink: /chemotaxis/home_senseadap
title: "Introduction to Chemotaxis"
sidebar:
 nav: "chemotaxis"
---

## Sensation

*E. coli* compares the **current vs. past** concentration of ligand and then controls the direction of flagellar rotation accordingly. We will deal with the *current* part first. To respond to the current concentration, the cells must be able to 1) sense the concentration; 2) respond accordingly.

The concentration is perceived by the cells by how many receptors are bound by ligand molecules.

[Visit Ligand-Receptor Dynamics Tutoiral](tutorial_lr){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

The rate of CheA autophosphorylation is dependent on **MCP-ligand binding**. When MCPs bind with attractants, rate of CheA autophosphorylation decreases, and thus CheY activity decrases, and flagellar CW rotation decrases, leading to less tumble. It is the opposite for the repellents.

[Visit Phosphorylation Tutoiral](tutorial_phos){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


## Adaptation

We will then deal with the *past* part. Consider -

*If one E. coli is in a well-mixed glucose solution with a concentration of A, and another is in a well-mixed glucose with a concentration of 10A, should they have the same tumbling frequency?*
 - Yes. If the second one tumbles less, it will have a harder time to move towards a even higher concentration.
 - The cell should go back to original tumbling frequency when no gradient presents despite what the concentration is.

*If one E. coli in glucose solution swam from A concentration to 10A concentration (assume it happened instantaneously), and another stays in a well-mixed glucose with a concentration of 10A, should they have the same tumbling frequency?*
 - No. The first one sensed a *change* in concentration, which indicates that if it keeps swimming in this direction, it might enter an area with higher concentration, so it should decrease tumbling frequency.
 - The cell should decide tumbling frequency based on the *change*, not the absolute concentration.

To achieve these, the cells should be able to record current concentration. This is achieved by **methylation states** (we will explain in more details in the tutorial). The rate of CheA autophosphorylation, besides MCP-ligand binding, is also dependent on **MCP methylation states**. Each MCP monomer has 4 methylation sites. Methylation reduces the negative charge on the receptors, making the receptor array packing more stable, thus increasing CheA autophosphorylation activities. When MCP has a higher methylation state, the rate of CheA autophosphorylation becomes higher.

Recall that CheB is methylated by phosphorylated CheA and is responsible for MCP methylation. When the cell first senses more ligand binding, the higher CheA phosphorylation would lead to more phosphorylated CheB, which then methylates MCPs. MCP records this sensed high concentration via high methylation state.

Therefore, when a cell reaches a region with higher attranctant concentration, initially CW rotation drops by the sensation mechanism, but then the higher CheB phosphorylation makes MCP methylation states higher, thus compensating for the increased binding and restoring tumbling frequencies.

The control of the 4 methylation sites are important to the precise adaptation mechanism[^Saragosti2001], but we will model a simpler version.

[Visit Adaptation Tutoiral](tutorial_adap){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


## Additional Resources

Some resources/reads if you are interested in the chemotaxis biology:
 - Amazing introduction to chemotaxis: Parkinson Lab [website](http://chemotaxis.biology.utah.edu/Parkinson_Lab/projects/ecolichemotaxis/ecolichemotaxis.html).
 - A good overview: by Webre et al. published in 2003. [Available online](https://www.cell.com/current-biology/pdf/S0960-9822(02)01424-0.pdf)
 - Details on chemotaxis pathway and MCPs: review article by Baker et al. published in 2005 [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/).
 - Details on MCPs: more recent review by Parkinson et al. published in 2015. [Available online](https://www.sciencedirect.com/science/article/abs/pii/S0966842X15000578).
 - Modeling robustness and integral feedback: lecture note by Berg in 2008. [Available online](https://www.weizmann.ac.il/mcb/UriAlon/sites/mcb.UriAlon/files/uploads/lecture_notes_-_robustness_in_bacterial_chemotaxis_.pdf).


[^Saragosti2001]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2001. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[Next Page: Gradient](home_gradient){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
