---
permalink: /chris/prediction
title: "Module 1: Title"
sidebar: 
 nav: "chris"
---


## Protein Structure Prediction

### How it Works
Currently, there are numerous software and publicly available servers that allow users to predict the protein structure of a given amino acid sequence. There are two main methods of structure prediction: template-based and *ab initio*. Template-based modeling can be further broken down to homology modeling and threading methods (fold-recognition). Homology modeling is based on the observation that proteins from the same evolutionary family with similar sequences typically adopt similar structures. By using homologous structures as a template, homology modeling often produces the most accurate results. While homology modeling usually requires the template and target to have notable sequence identity, threading does not have this limitation. This method creates structure predictions by placing or “threading” each amino acid in the target sequence to template structures from a constructed non-redundant template database, and then assessing how well it fits. Then, the best-fit templates are used to build the predicted model. Finally, *ab initio* prediction does not use templates, but rather Monte Carlo simulations based on an atomic-level force field. Due to the computational intensity and complexity of simulating folding, most software and servers limit the input sequence to be less than 200 residues with the high risk of producing low accuracy results.

[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](page2){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


