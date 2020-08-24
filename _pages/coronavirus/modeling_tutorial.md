---
permalink: /coronavirus/modeling_tutorial
title: "Protein Structure Prediction"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---
*Work in Progress*

Three protein prediction software were chosen for template-based modeling of the spike protein.

### SWISS-MODEL
<a href="https://swissmodel.expasy.org/" target="_blank">SWISS-MODEL</a> is a well-known structural bioinformatics web-server that specializes in homology modeling. The pipeline is comprised for four steps. 1) Using BLAST and HHblits, templates are identified and stored in the SWISS-MODEL Template Library. 2) The target sequence and template structure(s) are aligned. 3) Building the predicted models through a rigid fragment assembly approach. 4) Qualitiative Model Energy Analysis (QMEAN), a composite scoring function for model quality assessment. SWISS-MODEL was chosen to model the entire SARS-CoV-2 Spike protein and produced three models.

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/CoV2SpikeProteinSeq.txt" download>CoV-2 Spike Sequence </a>

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/SWISS_Model.zip" download> SWISS-MODEL Results </a>

### GalaxyWEB
<a href="http://galaxy.seoklab.org/" target="_blank">GalaxyWEB</a> is a web-server with many available services including protein structure prediction, structure refinement, protein interaction prediction, and GPCR applications. GalaxyTBM (the template-based modeling service) uses HHsearch to identify up to 20 templates, then aligns the core sequence with the templates using PROMALS3D. Next, models are generated using MODELLERCSA. GalaxyWEB was chosen to model the receptor binding domain (RBD) of the SARS-CoV-2 Spike protein and produced five models.

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/CoV2SpikeRBDSeq.txt" download>CoV-2 RBD Sequence </a>

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/GalaxyWEB_Models.zip" download> GalaxyWEB Results </a>

### Robetta
<a href="https://robetta.bakerlab.org/" target="_blank">Robetta</a> is a web-server that provides comparative and *ab initio* modeling of protein domains by utilizing the Rosetta fragment insertion method and de novo protocols. It allows for custom sequence alignments and can model multi-chain complexes. Robetta was chosen to model a single chain of the SARS-CoV-2 Spike protein and produced five models.

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/CoV2SpikeASeq.txt" download>CoV-2 Spike Chain A Sequence </a>

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/Robetta_Model.zip" download> Robetta Results </a>


[Return to main text](homology){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


