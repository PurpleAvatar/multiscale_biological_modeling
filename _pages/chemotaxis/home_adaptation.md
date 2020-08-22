---
permalink: /chemotaxis/home_senseadap
title: "Adaptation via Methylation"
sidebar:
 nav: "chemotaxis"
---

## Adaptation and Robustness

We will look at the other part of the story. Consider (think about optimal strategies) -

*If one E. coli is in a well-mixed glucose solution with a concentration of A, and another is in a well-mixed glucose with a concentration of 10A, should they have the same tumbling frequency?*
 - Yes. If the second one tumbles less, it will have a harder time to move towards a even higher concentration.
 - The cell should go back to original tumbling frequency when no gradient presents despite what the concentration is.

*If one E. coli in glucose solution swam from A concentration to 10A concentration (assume it happened instantaneously), and another stays in a well-mixed glucose with a concentration of 10A, should they have the same tumbling frequency?*
 - No. The first one sensed a *change* in concentration, which indicates that if it keeps swimming in this direction, it might enter an area with higher concentration, so it should decrease tumbling frequency.
 - The cell should decide tumbling frequency based on the *change*, not the absolute concentration.

To make decisions based on the *change* in concentration, the cells need to compare the **current vs. past** concentrations. In the last lesson, we've showed how ligand-receptor binding allow the cell to sense the current concentration, and we will deal about the past part here. The challenge is, since the presence of ligand means consistent stimulus, doesn't the cell need to respond consistently?

This is achieved via **adaptation** to the concentration (stimulus). When the stimulus persists at a constant level, the cell returns to background tumbling frequency, so that it can still detect the next change in concentration. Recall the biological oscillators model in the Motif Module, chemotaxis system's ability to return to the original state despite perturbation of the environment is another example of **robustness**. 

## Record past concentration through methylation

To do this, the cell records the past concentration. This is achieved by **methylation states**. **Methylation** is the chemical process of adding methyl group (-CH<sub>3</sub>) to an oraganic molecule. Such modification can change the activity of the molecules. The removal of a methyl group is called demethylation.

Our pathway will be based on the pathway explained on Parkinson Lab website. Illustration modified from Parkinson Lab illustration.[^ParkinsonLab]

The rate of CheA autophosphorylation, besides MCP-ligand binding, is also dependent on MCP methylation states. Each MCP monomer has 4 methylation sites. When more methylation sites on MCP are methylated, CheA autophosphorylation actvity becomes higher. There are two other proteins, **CheB**, which is phosphorylated by CheA and demethylates MCPs, and **CheR**, which methylates MCPs. Visualization below is modified from Parkinson Lab illustrations.[^ParkinsonLab]

 ![image-center](../assets/images/chemotaxis_methylation.png){: .align-center}
 <figcaption>A summary of the methylation pathway. CheA phosphorylates CheB. CheB methylates while CheR demethylates MCP. Blue curve: phosphorylation; grey curve: dephosphorylation; green arrow: methylation.</figcaption>

**CheB**. CheB is phosphorylated by CheA. CheB demethylates MCPs and readily autodephosphorylates. The rate of demethylation is dependent on MCP methylation states - faster to enter intermediate methylation levels[^Spiro1997].
 - CheA-P + CheB -> CheA + CheB-P
 - CheB-P -> CheB + P
 - MCP-Met + CheB-P -> MCP + CheB-P

**CheR**. CheR methylates MCPs. The rate of methylation is higher for ligand-bound receptors, and is higher for entering intermediate methylation levels[^Spiro1997].
 - MCP + CheR -> MCP-Met + CheR

Therefore, when a cell reaches a region with higher attranctant concentration, initially CW rotation drops via the phosphorylation cascade, but then the faster CheR-dependent methylation makes MCP methylation states higher. The higher methylation states make CheA autophosphorylation faster, compensating for more ligand-binding.

We will incorporate methylation in our pathway and have the whole story here. Illustration modified from Parkinson Lab illustration.[^ParkinsonLab]

 ![image-center](../assets/images/chemotaxis_wholestory.png){: .align-center}
 <figcaption>A summary of the whole story of chemotaxis pathways.Blue curve: phosphorylation; grey curve: dephosphorylation; green arrow: methylation.</figcaption>

[Visit Adaptation Tutoiral](tutorial_adap){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

From the BNG simulation, we can observe a fast response of CheY activity, and a slower adaptation that returns tumbling frequency to the background level. We can also observe that higher ligand concentration leads to stronger response, and higher level of steady state methylation.

L0 = 1e4.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e4.png){: .align-center}
L0 = 1e5.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e5.png){: .align-center}
L0 = 1e6.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e6.png){: .align-center}
L0 = 1e7.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e7.png){: .align-center}
L0 = 1e8.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e8.png){: .align-center}

We can see that the higher the concentration, the lower the valley becomes. But this is limited to a range of concentrations - going over a concentration where all receptors can already saturated instantly can't lead to more response; and a very low concentration won't initiate a response. Our results are also consistent with other simulations[^Bray1993] and experimental observations[^Shimizu2005][^Krembel2015]. 

In the Gradient section, we will see how the ability to respond to the change and adapt to the liigand concentration enable the cells to actually move up the gradient.

## Methylation states and Combinatorial Explosion

Why the methylation states can change CheA autophosphorylation actvities? Let's look at more MCP biochemistry.

 - There are five types of MCPs, Tsr, Tar, Tap, Trg, and Aer, specific for different species of ligand molecules. Most studies focus on the two most abundant types: Tsr (serine receptor) and Tar (aspartate and maltose receptor), and Aer (oxygen receptor) is less well understood.[^Parkinson2015] The MCPs form trimer of dimer structure. A trimer can be a mix of Tsr, Tar, Tap, Trg dimers. Binding with ligands changes the conformation of the receptor dimer. Each receptor dimer within the trimer impacts the activity differently because of asymmetricity in conformation.
 - MCPs, CheA (dimer with 5 subunits), and CheW forms receptor arrays. The receptor arrays generally have 2 states: 1) an ordered, dense state, in which CheA activity is higher; 2) a disordered, relaxed state, in which CheA activity is lower.[^Baker2005] The control of the 4 methylation sites and ligand-receptor binding impact array conformation are important to the precise adaptation mechanism[^Saragosti2001]. A visualization of the arrays from[^Yang2019] is shown below.

 ![image-center](../assets/images/chemotaxis_intro_tod.png){: .align-center}
 <figcaption>MCP array structures. From Yang et al.A)The trimer of dimer structure and changes of CheA autophosphorylation actvities depends on ligand binding and methylation states; P1...P5 are subunits of CheA. B)How MCPs, CheA, and CheW form receptor arrays.</figcaption>

 - Methylation reduces the negative charge on the receptors, making the receptor array packing more stable, thus increasing CheA autophosphorylation activities. When MCP has a higher methylation state, the rate of CheA autophosphorylation becomes higher.

That means our model is a very simplified version of the actual story. But can we actually build a more complete model?

We can add more receptor species and ligand species to account for the different attractants/repellents and their specific receptors easily. For each trimer of dimer, we will have more binding states and more methylation states, and include dependency of CheA autophosphorylation based on the newly added states. We will modify CheB and CheR reactions to account for 4 methylation sites. The rest can stay unchanged. Adding such complexity will require some coding, but is certainly doable.

The ability of including more complexity easily comes from the power of **rule-based modeling**. Specifying what the simulator should do only depends on the reaction rules, but not the state of the system. If we instead need to specify the states explicitly for the simulator, we will write an astronomical number of lines of code; imagine one typo somewhere.

## Additional Resources

Some resources/reads if you are interested in the chemotaxis biology:
 - Amazing introduction to chemotaxis: Parkinson Lab [website](http://chemotaxis.biology.utah.edu/Parkinson_Lab/projects/ecolichemotaxis/ecolichemotaxis.html).
 - A good overview: by Webre et al. published in 2003. [Available online](https://www.cell.com/current-biology/pdf/S0960-9822(02)01424-0.pdf)
 - Details on chemotaxis pathway and MCPs: review article by Baker et al. published in 2005 [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/).
 - Details on MCPs: more recent review by Parkinson et al. published in 2015. [Available online](https://www.sciencedirect.com/science/article/abs/pii/S0966842X15000578).
 - Modeling robustness and integral feedback: lecture note by Berg in 2008. [Available online](https://www.weizmann.ac.il/mcb/UriAlon/sites/mcb.UriAlon/files/uploads/lecture_notes_-_robustness_in_bacterial_chemotaxis_.pdf).


[^Munroe]: Randall Munroe. What If? [Available online](https://what-if.xkcd.com/)

[^Pierucci1978]: Pierucci O. 1978. Dimensions of *Escherichia coli* at various growth rates: Model of envelope growth. Journal of Bacteriology 135(2):559-574. [Available online](https://jb.asm.org/content/jb/135/2/559.full.pdf)

[^Sim2017]: Sim M, Koirala S, Picton D, Strahl H, Hoskisson PA, Rao CV, Gillespie CS, Aldridge PD. 2017. Growth rate control of flaggelar assembly in *Escherichia coli* strain RP437. Scientific Reports 7:41189. [Available online](https://www.nature.com/articles/srep41189#:~:text=Escherichia%20coli%20is%20a%20prominent,distributed%20across%20the%20cell%20surface.)

[^Baker2005]: Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)

[^Weis1990]: Weis RM, Koshland DE. 1990. Chemotaxis in *Escherichia coli* proceeds efficiently from different initial tumble frequencies. Journal of Bacteriology 172:2. [Available online](https://jb.asm.org/content/jb/172/2/1099.full.pdf)

[^Berg2000]: Berg HC. 2000. Motile behavior of bacteria. Physics today 53(1):24. [Available online](https://physicstoday.scitation.org/doi/pdf/10.1063/1.882934)

[^Achouri2015]: Achouri S, Wright JA, Evans L, Macleod C, Fraser G, Cicuta P, Bryant CE. 2015. The frequency and duration of *Salmonella* macrophage adhesion events determines infection efficiency. Philosophical transactions B 370(1661). [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4275903/)

[^Turner2016]: Turner L, Ping L, Neubauer M, Berg HC. 2016. Visualizing flagella while tracking bacteria. Biophysical Journal 111(3):630--639.[Available online](https://pubmed.ncbi.nlm.nih.gov/27508446/)

[^Parkinson2015]: Parkinson JS, Hazelbauer, Falke JJ. 2015. Signaling and sensory adaptation in *Escherichia coli* chemoreceptors: 2015 update. [Available online](https://www.sciencedirect.com/science/article/abs/pii/S0966842X15000578)

[^Yang2019]: Yang W, Cassidy CK, Ames P, Diebolder CA, Schulten K, Luthey-Schulten Z, Parkinson JS, Briegel A. 2019. *In situ* confomraitonal changes of the *Escherichia coli* serine chemoreceptor in different signaling states. mBio. [Available online](https://mbio.asm.org/content/10/4/e00973-19/article-info)

[^Saragosti2001]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2001. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[^Hlavacek2003]: Hlavacek WS, Faeder JR, Blinov ML, Perelson AS, Goldsten B. 2003. The complexity of complexes in signal transduction. Biotechnology and Bioengineering 84(7):783-94. [Available online](https://onlinelibrary.wiley.com/doi/abs/10.1002/bit.10842)

[^Hlavacek2006]: Hlavacek WS, Faeder JR, Blinov ML, Posner RG, Hucka M, Fontana W. 2006. Rules for modeling signal-transduction systems. Science Signaling 344:re6. [Available online](https://stke.sciencemag.org/content/2006/344/re6.long)

[^ParkinsonLab]: Parkinson Lab website. [website](http://chemotaxis.biology.utah.edu/Parkinson_Lab/projects/ecolichemotaxis/ecolichemotaxis.html)

[^Spiro1997]: Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).

[^Bray1993]: Bray D, Bourret RB, Simon MI. 1993. Computer simulation of phosphorylation cascade controlling bacterial chemotaxis. Molecular Biology of the Cell. [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC300951/)

[^Li2004]: Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^Stock1991]: Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^Shimizu2005]: Shimizu TS, Delalez N, Pichler K, and Berg HC. 2005. Monitoring bacterial chemotaxis by using bioluminescence resonance energy transfer: absence of feedback from the flagellar motors. PNAS. [Available online](https://www.pnas.org/content/103/7/2093/)

[^Krembel2015]: Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)

[Next Page: Gradient](home_gradient){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
