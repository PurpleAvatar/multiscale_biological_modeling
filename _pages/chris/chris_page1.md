---
permalink: /chris/prediction
title: "Module 1: Title"
sidebar: 
 nav: "chris"
---


## Protein Structure Prediction

### How it Works
Currently, there are numerous software and publicly available servers that allow users to predict the protein structure of a given amino acid sequence. There are two main methods of structure prediction: template-based and *ab initio*. Template-based modeling can be further broken down to homology modeling and threading methods (fold-recognition). Homology modeling is based on the observation that proteins from the same evolutionary family with similar sequences typically adopt similar structures. By using homologous structures as a template, homology modeling often produces the most accurate results. While homology modeling usually requires the template and target to have notable sequence identity, threading does not have this limitation. This method creates structure predictions by placing or “threading” each amino acid in the target sequence to template structures from a constructed non-redundant template database, and then assessing how well it fits. Then, the best-fit templates are used to build the predicted model. Finally, *ab initio* prediction does not use templates, but rather Monte Carlo simulations based on an atomic-level force field. Due to the computational intensity and complexity of simulating folding, most software and servers limit the input sequence to be less than 200 residues with the high risk of producing low accuracy results.

### Predicting the Structure of Sars-CoV-2 Spike Protein
Three protein prediction software were chosen for template-based modeling of the spike protein.
#### SWISS-MODEL
[SWISS-MODEL](https://swissmodel.expasy.org/) is a well-known structural bioinformatics web-server that specializes in homology modeling. The pipeline is comprised for four steps. 1) Using BLAST and HHblits, templates are identified and stored in the SWISS-MODEL Template Library. 2) The target sequence and template structure(s) are aligned. 3) Building the predicted models through a rigid fragment assembly approach. 4) Qualitiative Model Energy Analysis (QMEAN), a composite scoring function for model quality assessment. SWISS-MODEL was chosen to model the entire SARS-CoV-2 Spike protein and produced three models.
##### SARS-CoV-2 Spike Protein Sequence

>MGILPSPGMPALLSLVSLLSVLLMGCVAETGTQCVNLTTRTQLPPAYTNSFTRGVYYPDKVFRSSVLHSTQDLFLPFFSNVTWFHAIHVSGTNGTKRFDNPVLPFNDGVYFASTEKSNIIRGWIFGTTLDSKTQSLLIVNNATNVVIKVCEFQFCNDPFLGVYYHKNNKSWMESEFRVYSSANNCTFEYVSQPFLMDLEGKQGNFKNLREFVFKNIDGYFKIYSKHTPINLVRDLPQGFSALEPLVDLPIGINITRFQTLLALHRSYLTPGDSSSGWTAGAAAYYVGYLQPRTFLLKYNENGTITDAVDCALDPLSETKCTLKSFTVEKGIYQTSNFRVQPTESIVRFPNITNLCPFGEVFNATRFASVYAWNRKRISNCVADYSVLYNSASFSTFKCYGVSPTKLNDLCFTNVYADSFVIRGDEVRQIAPGQTGKIADYNYKLPDDFTGCVIAWNSNNLDSKVGGNYNYLYRLFRKSNLKPFERDISTEIYQAGSTPCNGVEGFNCYFPLQSYGFQPTNGVGYQPYRVVVLSFELLHAPATVCGPKKSTNLVKNKCVNFNFNGLTGTGVLTESNKKFLPFQQFGRDIADTTDAVRDPQTLEILDITPCSFGGVSVITPGTNTSNQVAVLYQDVNCTEVPVAIHADQLTPTWRVYSTGSNVFQTRAGCLIGAEHVNNSYECDIPIGAGICASYQTQTNSPSGAGSVASQSIIAYTMSLGAENSVAYSNNSIAIPTNFTISVTTEILPVSMTKTSVDCTMYICGDSTECSNLLLQYGSFCTQLNRALTGIAVEQDKNTQEVFAQVKQIYKTPPIKDFGGFNFSQILPDPSKPSKRSFIEDLLFNKVTLADAGFIKQYGDCLGDIAARDLICAQKFNGLTVLPPLLTDEMIAQYTSALLAGTITSGWTFGAGAALQIPFAMQMAYRFNGIGVTQNVLYENQKLIANQFNSAIGKIQDSLSSTASALGKLQDVVNQNAQALNTLVKQLSSNFGAISSVLNDILSRLDPPEAEVQIDRLITGRLQSLQTYVTQQLIRAAEIRASANLAATKMSECVLGQSKRVDFCGKGYHLMSFPQSAPHGVVFLHVTYVPAQEKNFTTAPAICHDGKAHFPREGVFVSNGTHWFVTQRNFYEPQIITTDNTFVSGNCDVVIGIVNNTVYDPLQPELDSFKEELDKYFKNHTSPDVDLGDISGINASVVNIQKEIDRLNEVAKNLNESLIDLQELGKYEQYIKGSGRENLYFQGGGGSGYIPEAPRDGQAYVRKDGEWVLLSTFLGHHHHHHHH


#### GalaxyWEB
[GalaxyWEB](http://galaxy.seoklab.org/) is a web-server with many available services including protein structure prediction, structure refinement, protein interaction prediction, and GPCR applications. GalaxyTBM (the template-based modeling service) uses HHsearch to identify up to 20 templates, then aligns the core sequence with the templates using PROMALS3D. Next, models are generated using MODELLERCSA. GalaxyWEB was chosen to model the receptor binding domain (RBD) of the SARS-CoV-2 Spike protein and produced five models.
##### SARS-CoV-2 RBD

>RVQPTESIVRFPNITNLCPFGEVFNATRFASVYAWNRKRISNCVADYSVLYNSASFSTFKCYGVSPTKLNDLCFTNVYADSFVIRGDEVRQIAPGQTGKIADYNYKLPDDFTGCVIAWNSNNLDSKVGGNYNYLYRLFRKSNLKPFERDISTEIYQAGSTPCNGVEGFNCYFPLQSYGFQPTNGVGYQPYRVVVLSFELLHAPATVCGPKKSTNLVKNKCVNFHHHHHH


#### Robetta
[Robetta](https://robetta.bakerlab.org/) is a web-server that provides comparative and *ab initio* modeling of protein domains by utilizing the Rosetta fragment insertion method and de novo protocols. It allows for custom sequence alignments and can model multi-chain complexes. Robetta was chosen to model a single chain of the SARS-CoV-2 Spike protein and produced five models.

##### SARS-CoV-2 Spike Protein Chain A

>ETGPNITNLCPFGEVFNATRFASVYAWNRKRISNCVADYSVLYNSASFSTFKCYGVSPTKLNDLCFTNVYADSFVIRGDEVRQIAPGQTGKIADYNYKLPDDFTGCVIAWNSNNLDSKVGGNYNYLYRLFRKSNLKPFERDISTEIYQAGSTPCNGVEGFNCYFPLQSYGFQPTNGVGYQPYRVVVLSFELLHAPATVCGPKKSTNKHHHHHH


### Structure Comparison with RMSD
RMSD is a common method to quantitatively measure the difference between two paired sets of values, such as coordinates. A lower RMSD value indicates a higher similarity between the two sets and a RMSD value of 0 indicates a perfect fit. This is especially useful in preliminary structure comparisons between proteins since protein structures are often represented as atomic coordinates. By comparing the RMSD between the predicted model the published model, a quantitative measure of the model's accuracy can be obtained. The formula for calculating RMSD is as follows:

<a href="https://www.codecogs.com/eqnedit.php?latex=\sqrt{\frac{1}{n}\sum_{n}^{i-1}d^{2}_{i}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sqrt{\frac{1}{n}\sum_{n}^{i-1}d^{2}_{i}}" title="\sqrt{\frac{1}{n}\sum_{n}^{i-1}d^{2}_{i}}" /></a>

where *n* is the number of pairs of equivalent atoms, *d* is the distance between the *i*th atom pair. For protein structure analysis, RMSD values are typically in the units of angstroms (Å). Proteins are made up of a chain of amino acids that is folded in a very specific way and the shape of the protein is vital to its function. Amino acids all have the same general structure: an amine group (-NH<sub>2</sub>), a carboxyl group (-COOH), a *R* group side-chain, and a central alpha-carbon (C⍺) that connects everything together. The amino acids are linked together by a peptide bond between the amine group of one amino acid and the carboxyl group of the other amino acid. By focusing on the positions of the alpha-carbons, the overall tertiary shape can be determined, although this leaves out the *R* groups, which is extremely important since they are responsible for the biochemical properties of the amino acids, and the folding and interactions of the protein. However, the alpha-carbons are usually sufficient in preliminary structure comparison assessments and for calculating RMSD.


[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](rmsd_prody){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


