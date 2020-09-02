---
permalink: /coronavirus/tutorial_ab_initio
title: "Ab initio Structure Prediction Tutorial"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

* *Ab initio* structure prediction is the method of predicting the 3D structure (tertiary structure) of a protein using only its amino acid sequence (primary structure) and physicochemical interactions. This means that previously determined structures are not used as templates or guides to help in this process. In a sense, *ab initio* structure prediction is solving nature's "magic algorithm" of protein folding that was introduced in <a href="structure_intro">Introduction to Protein Structure Prediction</a>.

* Because this type of structure prediction is incredibly difficult and computationally intensive, there are still many problems with current *ab initio* algorithms. Perhaps one of the largest setbacks is that current algorithms severely limit the length of the input sequence. For example, the leading *ab initio* modeling algorithm *QUARK* limits the input to only 200 amino acids. As a result, we are not even allowed the opportunity to use *ab initio* structure prediction on the RBD of SARS-CoV-2 (about 229 amino acids long according to PDB entry <a href="https://www.rcsb.org/structure/6M0J" target="_blank">6m0j</a>), let alone the entire S protein.

* Nevertheless, we can use *QUARK* to try to model the much smaller protein <a href="https://www.rcsb.org/structure/1nxb" target="_blank">1nxb</a>, a 62 amino acid neurotoxin from the black-banded sea krait.

**Results are pending**

[Return to main text](ab_initio){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
