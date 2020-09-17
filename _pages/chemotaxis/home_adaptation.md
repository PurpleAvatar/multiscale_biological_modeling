---
permalink: /chemotaxis/home_senseadap
title: "Methylation Helps Bacteria Adapt to Differing Concentrations"
toc: true
toc_sticky: true
sidebar:
 nav: "chemotaxis"
toc: true
toc_sticky: true
---

## Bacterial tumbling frequencies remain constant despite background attractant concentrations

In the previous lesson, we explored the signal transduction pathway by which *E. coli* can change its tumbling frequency in response to a change in the concentration of an attractant. But the reality of cellular environments is that the concentration of a substance in these environments can vary across several orders of magnitude. The cell therefore needs to detect not *absolute* concentrations of attractant or repellent but rather *relative* changes in its environment so that it can move in the direction of an attractant (or away from a repellent).

For example, consider two bacterial cells, both of which are in well-mixed environments with fixed glucose concentrations. The first cell's environment has a glucose concentration of *x*, and the second cell's environment has a glucose concentration of 10*x*. Should the tumbling frequency of the second cell be lower?  What if we drop a sugar cube into both environments?  Shouldn't both cells be able to respond in the same way in response to this attractant?

The ability of *E. coli* to react to relative changes in its environment is not  present in our current model of chemotaxis. According to our current model, if a cell is in an environment with high background concentration of an attractant, then the cell will detect a signal and lower its tumbling frequency. If the concentration continues to increase, then it may not be able to lower this frequency any further.

*E. coli* detects relative changes in its concentration via **adaptation** to the signal concentration. If the concentration of attractant remains constant for a period of time, then *regardless* of the absolute value of the concentration, the cell returns to the same background tumbling frequency. The ability of *E. coli* to maintain its default tumbling behavior across varying concentrations of attractant offers another example of the principle of *robustness* that we introduced earlier in this course. In this lesson, we will investigate the biochemical mechanism that *E. coli* uses to achieve such a robust response to variable environments, and then we will further expand our BioNetGen model to see if it can replicate this adaptive response.

## Bacteria have a "memory" of past concentrations using methylation

Recall from the last section that in the absence of an attractant, CheW and CheA readily bind to an MCP, leading to greater autophosphorylation of CheA, which in turn phosphorylates CheY. The greater the concentration of phosphorylated CheY, the more frequently the bacterium tumbles.

Signal transduction was achieved through phosphorylation, but *E. coli* maintains a *memory* of past environmental concentrations through a chemical process called **methylation**. In this  reaction, a **methyl group** (-CH<sub>3</sub>) is added to an organic molecule; the removal of a methyl group is called **demethylation**.

Every MCP cellular receptor contains four methylation sites, meaning that between zero and four methyl groups can be added to the receptor. On the plasma membrane, many MCPs, CheW, and CheA molecules form an array structure. Methylation reduces the negative charge on the receptors, stabilizing the array and facilitating CheA autophosphorylation. The more sites that are methylated, the higher the autophosphorylation rate of CheA, which means that CheY has a higher phosphorylation rate, and tumbling frequency increases.

We now have two different ways that tumbling frequency can be elevated. First, if the concentration of an attractant is low, then CheW and CheA freely form a complex with the MCP, and the phosphorylation cascade passes phosphoryl groups to CheY, which interacts with the flagella and keeps tumbling frequency high. Second, an increase in MCP methylation can also boost CheA autophosphorylation and lead to an increased tumbling frequency.

Methylation of MCPs is achieved by an additional protein called **CheR**. When bound to MCPs, CheR methylates ligand-bound MCPs faster[^Amin2010][^Terwilliger1986], so the rate of MCP methylation by CheR is higher if the MCP is bound to a ligand.[^Spiro1997]. Therefore, say that *E. coli* encounters an increase in attractant concentration. Then the lack of a phosphorylation cascade will mean that there is less phosphorylated CheY, and so the tumbling frequency will decrease. However, if the attractant concentration levels off, then the tumbling frequency will flatten, while CheR starts methylating the MCP. Over time, the rising methylation will increase CheA autophosphorylation, bringing back the phosphorylation cascade and raising tumbling frequency back to default levels.

<!--
![image-center](../assets/images/chemotaxis_methylation.png){: .align-center}
<figcaption>The chemotaxis signal-transduction pathway with methylation included. CheA phosphorylates CheB. CheB methylates while CheR demethylates MCP. Blue curve: phosphorylation; grey curve: dephosphorylation; green arrow: methylation. Figure inspired by Parkinson Lab illustrations.[^ParkinsonLab]</figcaption>
-->

<!--
 - MCP + CheR -> MCP-CH<sub>3</sub> + CheR
 - CheA-P + CheB -> CheA + CheB-P
 - CheB-P -> CheB + P
 - MCP-CH<sub>3</sub> + CheB-P -> MCP + CheB-P
-->

Just as the phosphorylation of CheY can be undone, MCP methylation can be undone as well to prevent methylation from being permanent. In particular, an enzyme called **CheB**, which like CheY is phosphorylated by CheA, demethylates MCPs (as well as autodephosphorylates). The rate of an MCP's demethylation is dependent on the extent to which the MCP is methylated. In other words, the rate of MCP methylation is higher when the MCP is in a low methylation state, and the rate of demethylation is faster when the MCP is in a high methylation state.[^Spiro1997]

The figure below adds CheR and CheB to provide a complete picture of the core pathways influencing chemotaxis. In order to model these pathways, we will need to add quite a few molecules and reactions to our current model. In the tutorial linked below, we will expand the BioNetGen model that we built in the previous lesson, and then see if this model can replicate the adaptation behavior of *E. coli* within a changing attractant concentration.

 ![image-center](../assets/images/chemotaxis_wholestory.png){: .align-center}
 <figcaption>The chemotaxis signal-transduction pathway with methylation included. CheA phosphorylates CheB, which methylates an MCP while CheR demethylates MCP. Blue lines denote phosphorylation, grey lines denote dephosphorylation, and the green arrow denotes methylation. Figure inspired by Parkinson Lab illustrations.[^ParkinsonLab]</figcaption>

## Combinatorial explosion and the need for rule-based modeling

Before incorporating the adaptation mechanisms in our BNG model, let's write out the reactions first. 

Start with MCP complexes. In the [phosphorylation tutorial](tutorial_phos), we identified two components relevant for reactions involving MCPs: a ligand-binding component `l` and a phosphorylation component `Phos`. The adaptation mechanism introduces additional reactions: methylation by CheR, and demethylation by CheB. We also need to include the binding-dissociation with CheR because under normal conditions, most CheR are bound to MCP complexes [^Lupas1989]. Thus we can introduce two additional components, `r` for CheR-binding, and `Meth` for methylation states. In our simulation, we will use 3 methylation levels, low, medium, and high because 3 methlytion states are most invovled in the chemotaxis to attractants [^Boyd1980].

When writing the code for a reaction, we need to specify each species involved. To specify an MCP here, we will need to tell the program the exact state it is at, i.e., whether bound to a ligand, whether bound to CheR, whether phosphorylated, and which methylation state it has. Therefore, there are 2 · 2 · 2 · 3 = 24 possible states for an MCP. 

When writing the reaction of a ligand molecule binds to an MCP, we select the MCPs not bound to a ligand yet, and there are 1 · 2 · 2 · 3 = 12 states that allow this binding reaction.

When writing the reaction of a CheR molecule binds to an MCP, we select the MCPs not bound to a CheR yet, and there are 2 · 1 · 2 · 3 = 12 possible states.

When writing the reaction of an MCP at methlylation state A gets methylated by a CheR molecule, the reaction rate also depends on whether the MCP is bound to a ligand molecule, so we have 1 · 1 · 2 · 1 + 1 · 1 · 2 · 1 = 4 reactions. Similarly an MCP at methlylation state B gets methylated requires us to specify 4 reactions.

And we need to specify reactions for demethylation, phosphorylation, ... How can I debug if there is a typo...

But do we really need that many reactions? When we model ligand-MCP binding, we don't care the MCP is phosphorylated or not, bound to CheR or not, or its methylation state. We only care about the reactive part - it is not bound to a ligand molecule yet. So our 12 reactions can simplify to 1 reaction rule: a free ligand molecule binds to an MCP that is not bound to a ligand molecule. Why is one rule enough? Recall in [Gillespie algorithm](/home_signal), the wait time before the next reaction and which reaction happen next only depends on the rate of all reactions in the system. The rate of ligand-MCP binding depends on the total concentration of free ligands and MCPs not bound to ligand, but not MCPs' other states.

Similarly, when modeling MCP-CheR binding, we don't care anything except the MCP is not bound to a CheR molecule yet. The 12 possible reactions become 1 too. When modeling methylation, we only need 1 reaction for each combination of states that impacts the rate constant. No more worries about typing out dozens of lines of code that only differ by one word. The problem of specifying the states is circumvented by representing reactions in local rules.[^Chylek2015]

As you might have realized, BNG takes advantage of such **rule-based modeling**. In our simulations, we will only worry about the components that are involved in a particular reactions, or influence the rate constant of that reaction.

[Visit tutorial](tutorial_adap){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## New subsection

In the figures below, we show plots of the concentration of each molecule in the system under a few different circumstances. In each case, we suddenly change the concentration of an attractant ligand and examine how this affects the concentration of phosphorylated CheY (the molecule that influences the tumbling frequency). Will the model reflect our biochemical hypothesis that *E. coli* can return to approximately the same steady-state concentration of phosphorylated CheY regardless of the concentration of the ligand?

Here we show simulation results for some different amounts of ligand molecules suddenly added at the beginning of the simulation. First a relatively small amount, by setting `L0 = 1e4`.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e4.png){: .align-center}
We gradually increase the amount of ligand molecules added. With `L0 = 1e5`.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e5.png){: .align-center}
With `L0 = 1e6`.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e6.png){: .align-center}
With `L0 = 1e7`.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e7.png){: .align-center}
With `L0 = 1e8`.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e8.png){: .align-center}

We can see that the higher the concentration, the deeper the drop of phosphorylated CheY can be observed.

But this is limited to a range of concentrations - going over a concentration where all receptors can already saturated instantly can't lead to more response; and a very low concentration won't initiate a response. Our results are also consistent with other simulations[^Bray1993] and experimental observations[^Shimizu2005][^Krembel2015].

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

[^Amin2010]: Amin DN, Hazelbauer GL. 2010. Chemoreceptors in signaling complexes: shifted conformation and asymmetric coupling. [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3010867/)

[^Terwilliger1986]: Terwilliger TC, Wang JY, Koshland DE. 1986. Kinetics of Receptor Modification - the multiply methlated aspartate receptors involved in bacterial chemotaxis. The Journal of Biolobical Chemistry. [Available online](https://www.jbc.org/content/261/23/10814.full.pdf)

[^Chylek2015]: Chylek LA, Harris LA, Tung CS, Faeder JR, Lopez CF, Hlavacek WS. 2015. Rule-based modeling: a computational approach for studying biomolecular site dynamics in cell signaling systems. Wiley Interdiscip Rev Syst Biol Med 6(1):13-36. [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3947470/)

[^Boyd1980]: Boyd A., and Simon MI. 1980. Multiple electrophoretic forms of methyl-accepting chemotaxis proteins generated by stimulus-elicited methylation in Escherichia coli. Journal of Bacteriology 143(2):809-815. [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC294367/pdf/jbacter00569-0269.pdf)

[^Lupas1089]: Lupas A., and Stock J. 1989. Phosphorylation of an N-terminal regulatory domain activates the CheB methylesterase in bacterial chemotaxis. J Bio Chem 264(29):17337-42. [Available online](https://pubmed.ncbi.nlm.nih.gov/2677005/)

[Next lesson](home_gradient){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
