---
permalink: /coronavirus/homology
title: Homology Modeling for Protein Structure Prediction
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

* Although a perfected *ab initio* protein structure prediction remains out of reach, there is another more popular, more accurate approach to structure prediction. As mentioned in the *Introduction to Protein Structure Prediction* section, we have over 160,000 protein structure entries available in the PDB. With every new structure we identify, we learn a little more about the rules that nature uses to fold proteins into shapes. So, why not leverage this database in predicting structures? This is exactly how homology modeling and other template-based methods approach structure prediction.

* Homology modeling is based on the observation that proteins from the same evolutionary family with similar sequences typically adopt similar structures. Using sequence comparisons, we can scour the database for proteins with notable sequence identity to be used as a template. Now that we have a starting point, the chances of predicting the correct structure is greatly improved, as well as potentially speeding up the process.

* Unfortunately, there are occasions where no identified proteins have notable sequence similarities. The alternative is to use threading, or fold recognition. In this case, rather than aligning sequence to sequence, this method aligns sequence to structures. The biological basis of this method is that in nature, protein structures tend to be highly conservative and unique structural folds are therefore limited. (If it ain’t broke… Of course, mutations and structure deviations occur over evolutionary timeline.) A simple explanation of the general threading algorithm is that structure predictions are created by placing or “threading” each amino acid in the target sequence to template structures from a non-redundant template database, and then assessing how well it fits with some scoring function. Then, the best-fit templates are used to build the predicted model. The scoring function varies per algorithm, but it typically takes secondary structure compatibilities, gap penalties during alignment, and other terms that depend on amino acids that are bought into contact by the alignment.

  * More information on threading scores can be found <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3244815/" target="_blank">here</a>.

* I-TASSER, developed by the Yang Zhang Lab, is a successful structure prediction that uses the threading method LOMETS for template construction. The method first identifies structural templates and fragments of super-secondary structures from non-redundant PDB. Then, using replica-exchange Monte Carlo simulations, many templates are created. SPICKER clustering is then used to find the cluster centroid for template usage.

  * The full description of I-TASSER can be found <a href="http://europepmc.org/backend/ptpmcrender.fcgi?accid=PMC2849174&blobtype=pdf" target="_blank">here</a>.
  
<img src="../_pages/coronavirus/files/ITASSER.png">

* Going back to the analogy of the newly discovered planet from the previous section, where a droid, our protein structure predictor, is rolling across the extremely uneven surface of the planet, which represents all the possible structure conformations with altitudes based on the conformation energy. We know that the correct native form of the protein has a low energy conformation, so the droid will need to find the location of the lowest-lying area. Unfortunately, there are two major problems:
  * The surface is covered with large craters.
  * The deeper we go into the crater, the flatter the curvature.
  With no prior knowledge other than the fact that the answer is located at the lowest altitude, we can only explore the craters thoroughly and hope we get lucky. This scenario is most like that of *ab initio* modeling. 

* Let’s say that we have explored many planets of similar topography and we have a database containing the description of every planet and which crater lowest-lying area is. We can search the database for the planet most similar to the current one and use it as a guide (a template) to narrow down which craters to explore. This scenario is most like that of homology modeling and other template-based approaches.

<hr>

If you would like to learn more about protein structure prediction, click here to see how we used three publically available protein prediction software to model SARS-CoV-2 S protein.

[Tutorial](tutorial_homology){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

<hr>

[Next lesson](accuracy){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}






