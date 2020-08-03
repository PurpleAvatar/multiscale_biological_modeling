---
permalink: /coronavirus/RMSD_results
title: "Assessing Accuracy of Models"
sidebar: 
 nav: "coronavirus"
---
Now that we have the predicted models of the full Spike protein (SWISS), RBD (GalaxyWEB), and single chain (Robetta), we need a way to assess their accuracy.

### Structure Comparison with RMSD
RMSD is a common method to quantitatively measure the difference between two paired sets of values, such as coordinates. A lower RMSD value indicates a higher similarity between the two sets and a RMSD value of 0 indicates a perfect fit. This is especially useful in preliminary structure comparisons between proteins since protein structures are often represented as atomic coordinates. By comparing the RMSD between the predicted model the published model, a quantitative measure of the model's accuracy can be obtained. The formula for calculating RMSD is as follows:

<a href="https://www.codecogs.com/eqnedit.php?latex=\sqrt{\frac{1}{n}\sum_{n}^{i-1}d^{2}_{i}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sqrt{\frac{1}{n}\sum_{n}^{i-1}d^{2}_{i}}" title="\sqrt{\frac{1}{n}\sum_{n}^{i-1}d^{2}_{i}}" /></a>

where *n* is the number of pairs of equivalent atoms, *d* is the distance between the *i*th atom pair. For protein structure analysis, RMSD values are typically in the units of angstroms (Å). Proteins are made up of a chain of amino acids that is folded in a very specific way and the shape of the protein is vital to its function. Amino acids all have the same general structure: an amine group (-NH<sub>2</sub>), a carboxyl group (-COOH), a *R* group side-chain, and a central alpha-carbon (C⍺) that connects everything together. The amino acids are linked together by a peptide bond between the amine group of one amino acid and the carboxyl group of the other amino acid. By focusing on the positions of the alpha-carbons, the overall tertiary shape can be determined, although this leaves out the *R* groups, which is extremely important since they are responsible for the biochemical properties of the amino acids, the folding of the protein, and its interactions. However, the alpha-carbons are usually sufficient in preliminary structure comparison assessments and for calculating RMSD.

### RMSD of the Models
For each of the three types of predicted models, the RMSD between each other, SARS-CoV-2 structures from PDB, and SARS structures from PDB were calculated using ProDy. Along with the SWISS models, five predicted models of the entire Spike protein that were released by <a href="https://boinc.bakerlab.org/" target="_blank">Rosetta@Home</a> to the *Seattle Structural Genomics Center for Infectious Disease* (SSGCID) were also assessed. Because these SSGCID models were produced using greater computational power than SWISS, comparing the RMSD of the two sets of models will provide more insight on the effect of computational power on accuracy. The SSGCID models can be found <a href="https://www.ssgcid.org/cttdb/molecularmodel_list/?target__icontains=BewuA" target="_blank">here</a>. The published PDB models are as follows: <a href="https://www.rcsb.org/structure/6vxx" target="_blank">6vxx</a> (for SARS-CoV-2 whole Spike and single chain), <a href="https://www.rcsb.org/structure/6CRX" target="_blank">6crx</a> (for SARS whole Spike and single chain), <a href="https://www.rcsb.org/structure/6lzg" target="_blank">6lzg</a> (for SARS-CoV-2 RBD), and <a href="https://www.rcsb.org/structure/6waq" target="_blank">6waq</a> (for SARS RBD).

For whole Spike modeling, the RMSD between SARS-CoV-2 and SARS is 11.368. Looking at the SWISS models, the best performing model with SARS-CoV-2 is 5.8518, while the worst is 11.3432. In comparison, the best performing SSGCID model to 6vxx is 2.08537 and the worst being 4.9636.

<img src="../_pages/coronavirus/files/RMSD_result/Swiss/">
<img src="../_pages/coronavirus/files/RMSD_result/SSGCID/">

For RBD modeling, the RMSD between SARS-CoV-2 and SARS is 2.0072. The best performing GalaxyWEB model RMSD with SARS-CoV-2 is 0.1202 and the worst being 0.1526.

<img src="../_pages/coronavirus/files/RMSD_result/Galaxy/">

For single chain modeling, the RMSD between SARS-CoV-2 and SARS is 10.936. The best performing Robetta model RMSD with SARS-CoV-2 is 2.5852 and the worst being 12.0975.

<img src="../_pages/coronavirus/files/RMSD_result/Robetta/">

Looking at the RMSD values, SSGCID models far outperformed the models produced by SWISS. Although this may be due to a number of factors (e.g. different algorithms), one main factor is that the SSGCID modesl took much more computational power and time, which supports a positive correlation between computational power and accuracy. The difference between the best and worst GalaxyWEB models and high RSMD values between predicted models (e.g. 29.7861 between SSGCID_1 and SSGCID_4), indicate the potential of large variability between produced models. Lastly, there appears to be a negative correlation between sequence length and prediction accuracy for protein predictions of similar compuational power, where RBD models performed the best, followed by single chain models, and whole Spike models (SWISS) performing the worst.

To see the full RMSD report with RMSD values between the predicted models, download the results <a href="/multiscale_biological_modeling/_pages/coronavirus/files/RMSD_result/RMSD_Results.csv" download>here</a>.

[Previous](prediction){: .btn .btn--primary .btn--x-large} [Next Page](rmsd2){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
