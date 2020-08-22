---
permalink: /coronavirus/ab_initio
title: Ab initio Protein Structure Prediction
sidebar:
 nav: "coronavirus"
toc: true
toc_sticky: true
---

* The final goal is to be able to accurately determine the structure of a protein from just the primary structure, *ab initio* structure prediction. *Ab initio* is Latin for “from the beginning”.
* Extremely difficult to do, essentially all *ab initio* algorithms utilize information from structural and sequence databases in some form to fill holes. Relies entirely on physiochemical interactions.

## Levinthal's Paradox

* Levinthal’s Paradox. Large number of degrees of freedom in a polypeptide chain. Given a chain with 100 residues, there will be 99 peptide bonds, resulting in 198 phi and psi bond angles. If each bond has three stable conformations, then there are a maximum of $$ 3^[198] $$ different possible conformations. Will take longer than the age of the universe to sample all conformation to find the correct native form. Paradox is that most natural protein folding occurs spontaneously, typically within the timescale of milliseconds. The fastest within a couple of microseconds [^1].
  * Local residues form stable interactions an act as nucleation points (protein folding intermediates and partial-folded transition states), facilitation folding speed.
  * Proposed funnel-like energy landscapes (not really the case, the energy landscape is more like a caldera).
  * Main point: need A LOT of computing 
  
## CAPS, Rosetta, and QUARK

* Critical Assessment of Structure Prediction (CASP) experiments are held every two years. It is a community-wide/world-wide double-blind protein structure prediction experiment that helps research groups across the world to objectively test their prediction software and algorithm for all types of predictions.

* For CASP6 in 2004, Rosetta, the program used by <a href="https://boinc.bakerlab.org/rosetta/" target="_blank">Rosetta@home</a> was the first produce a near atomic-level resolution *ab initio* prediction for its model of the CASP target T0281. Ever since, Rosetta has been one of the leading predictors, placing among the top in every category of structure prediction in CASP7. One aspect that contributes greatly to Rosetta’s success is the amount of computer power made available by Rosetta@home volunteers. (Run Rosetta@home when the user is not using the computer, donating idle computer power). Amid the COVID-19 pandemic, the Rosetta@home recruited thousands of volunteers around the world to help model important SARS-CoV-2 proteins, including the S protein, before the proteins could be measured in the lab.
  * An article about Rosetta’s role: https://www.ipd.uw.edu/2020/02/rosettas-role-in-fighting-coronavirus/). 
  * Models published before crystallography can be found here: https://www.ssgcid.org/cttdb/molecularmodel_list/?target__icontains=BewuA

* QUARK is one of the leading *ab initio* protein structure prediction available. As mentioned before, currently employed *ab initio* modeling is not truly *ab initio*. We still utilize data from previously determined structures in some form. However, the database that is used is not required to contain structures that are similar in global structure. Very short fragments of the known structures are used to construct the model rather than using entire proteins as templates. In addition, extensive physiochemical knowledge is needed. Here is a flow chart of QUARK:

<img src="../_pages/coronavirus/files/QuarkFlowChart.png">

## How *Ab initio* Structure Prediction Works

* As mentioned in the figure, many potential models, or decoys, are created. To select the best performing model, a scoring function is used. Many different scoring functions are used, some combining multiple types of scoring, and generally fall into one of two categories: consensus or clustering. Simply put, consensus follows the idea that the more common the predicted conformations are, the more likely it is to be correct as opposed to structural patterns that are rarely found. On the other hand, clustering methods are much more complicated. Commonly used clustering basis includes stereochemical plausibility of the models, environmental compatibility of the residues, and energy-based calculations such as physics-based functions and knowledge-based statistical potentials [^2].

* Regardless of the different *ab initio* modeling approaches, it ultimately boils down to solving the problem of finding the 3-D shape of a protein sequence that maximizes some scoring function, where the scoring function indicates how good the 3-D shape is at explaining the sequence. However, one of the important guidelines in protein folding, both in modeling and in biology, is obtaining a low-energy conformation. A general theme in chemistry is that systems move spontaneously towards equilibrium, or stable state, be it a chemical reaction or a molecule itself. When a system is at equilibrium, it is typically in its lowest possible energy state, or minimum free energy. Think of a high energy system as a ball on top of a round mountain. The ball will always roll down the hill and stop at the bottom of the valley, where it is the most stable.

* In protein structure prediction, the path to the best model is not a straight line. Common approaches often have steps for model refinement. When models are first generated, they are assessed and used to create better models. Although time consuming and computationally heavy, the more times we can repeat this cycle, the better the final product. Approaches for ab initio modeling used are not dissimilar from the biased random walk approach that E. coli uses to explore its space for food. In this case, the “search space” is not a physical space but rather the set of all legal structures of the protein for this structure. The “food” is not the current concentration of an attractant but the current score of a candidate structure. And “nearby” objects are not points in space but rather 3-d protein structures that correspond to making slight changes to the current structure.

* High-level description of the general algorithm:
  * Start with an arbitrary protein structure.
  * Consider all its possible neighbors. Is there one with a score better than the current structure?
  * If yes, update the current structure to the highest scoring neighbor and repeat the previous step.
  * If not, return the current structure as the best one found

**STOP:** Are there any drawbacks you see with this approach for predicting a protein’s structure?
{: .notice--primary}

* The most glaring weakness is that the initial structure chosen can have a huge influence on the final structure that we produce.  As a result, we can get stuck in a “local optimum”, in this case a protein structure that is higher scoring than its neighbors but that doesn’t score very well compared to all possible structures.

* Let's say we are exploring a newly discovered planet with a droid that can roll over the surface of the planet. If the droid is looking for the lowest-lying area on the planet by moving in the direction of greatest descent, and it lands at the top of a volcano, it will roll down into the volcano’s cauldron, which is still very high compared to the rest of the planet. One resolution to this issue is to run the algorithm multiple times with different starting positions, choosing the solution that has the best score over all these runs. Another solution is to not necessarily always take the best-scoring neighbor as the next current protein structure, but rather to choose a neighbor randomly, where higher-scoring neighbors have a higher probability of selection. 

Randomness appears once again!

[Next lesson](nar){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Citations

[^1]: Kubelka, J., et. al. 2004. The protein folding ‘speed limit’. Current Opinion in Structural Biology. 14, 76-88. https://doi.org/10.1016/j.sbi.2004.01.013

[^2]: Benkert, P., Schwede, T. & Tosatto, S.C. 2009. QMEANclust: estimation of protein model quality by combining a composite scoring function with structural density information. BMC Struct Biol 9, 35. https://doi.org/10.1186/1472-6807-9-35