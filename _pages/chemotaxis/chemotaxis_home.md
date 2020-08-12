---
permalink: /chemotaxis/home
title: "Introduction to Chemotaxis"
sidebar:
 nav: "chemotaxis"
---

### by Shuanger Li and Phillip Compeau

## Lost Immortals

The book *What If?*[^1] compiles a collection of crazy hypotheticals, along with enthusiastically scientific replies from the author. Below is one such quandary:

> If two immortal people were placed on opposite sides of an uninhabited Earth-like planet, how long would it take them to find each other? 100,000 years? 1,000,000 years?

**STOP:** What would you propose that the two immortals could do to find each other?

* Solution from book is below. Need to discuss this solution in the context of what comes before (there are thoughts to go to the coastlines. You could also decide to meet each other at the North Pole if you could discuss in advance.) Munroe describes his approach as "be an ant". Ants also use this type of random walk strategy.

> If you have no information, walk at random, leaving a trail of stone markers, each one pointing to the next. For every day that you walk, rest for three. Periodically mark the date alongside the cairn. It doesn’t matter how you do this, as long as it’s consistent. You could chisel the number of days into a rock, or lay out rocks to plot the number.
>
> If you come across a trail that’s newer than any you’ve seen before, start following it as fast as you can. If you lose the trail and can’t recover it, resume leaving your own trail.
>
> You don’t have to come across the other player’s current location; you simply have to come across a location where they’ve been. You can still chase one another in circles, but as long as you move more quickly when you’re following a trail than when you’re leaving one, you’ll find each other in a matter of years or decades.
>
> And if your partner isn’t cooperating—perhaps they’re just sitting where they started and waiting for you—then you’ll get to see some neat stuff.

* What is the point of this introduction? Discuss the power of randomness that we have already repeatedly seen throughout the book. Then point out that although randomness is useful for running simulations, it is also useful as an algorithm for finding things.

* The above algorithm for two people finding each other in a crazy hypothetical is in fact inspired by nature. It is described by Munroe as "be an ant" and is similar to the approach that ants take to explore their world.

* We will look at a related example of using random walks as an effective means of exploring one's environment: bacterial chemotaxis. (Transition to chemotaxis.)

## Introduction to Chemotaxis

Like other prokaryotes, *E. coli* are small, with a length about 2µm, and a diameter 0.25-1µm.[^2] This puts them into the same situation like the Lost Immortals or the ants exploring the world: the environment in which they need to find food is huge; food is sparsely distributed; and they are small. The answer is the chemotaxis behavior.

The behavior of cells moving towards or away from a substance is called **chemotaxis**. For *E. coli*, moving towards attractants (ex. glucose, electron acceptors), and moving away from repellents (ex. Ni<sup>2+</sup>, Co<sup>2+</sup>) are all considered chemotaxis behaviors.

Here is a cute video of *E. coli* moving towards a sugar crystal.
<iframe width="640" height="360" src="https://www.youtube.com/embed/F6QMU3KD7zw" frameborder="0" allowfullscreen></iframe>

## How does *E. coli* explore the world?

*E. coli* has 5-12 flagelli randomly distributed in the surface.[^3] Each flagelum rotates clockwise (CW) or counter-clockwise (CCW). That leads to two states of movement: 1) when flagelli rotates in CCW, they form a bundle, and propel the cells to swiming smoothly at speeds of 20 µm per second, called **run**; 2) when some flaggeli in the bundle rotates CW, the flagelli become uncoordinated and reorients with a much slower net movement speed in place, called **tumble**.[^4]

![image-center](../assets/images/chemotaxis_intro_runtumble.png){: .align-center}
(Image from Parkinson Lab, University of Utah)

In a uniform environment, *E. coli* tumbles once about every 1-1.5 seconds.[^5][^6] Such tumbling frequency is clever, because if the bacteria tumble too much, it won't be able to explore the space; but if it tumbles too little, it might go too far in the wrong direction. Other flagellated motile bacteria uses similar exploration mechanisms; for example, *Salmonella* bacteria tumbles about once per second[^7], *Bacillus subtilis* tumbles about every 2 seconds, *Enterococcus sacchrolyticus* tumbles about per 1.2 seconds.[^8]

## Biochemistry

*E. coli* run and tumble is controlled by a series of chemotaxis proteins. This figure summarizes the signaling pathway.
![image-center](../assets/images/chemotaxispathway.jpg){: .align-center}
(Image from Parkinson Lab, University of Utah)

Detailed explanation of the pathway:

**Receptor Complexes**. On the cell membrane, there are receptors called **methyl-acceptring chemotaxis proteins (MCPs)**. They form complexes with **CheW** and **CheA** (*Che* stands for chemotaxis).
 - There are five types of MCPs, Tsr, Tar, Tap, Trg, and Aer, specific for different species of ligand molecules. Most studies focus on the two most abundant types: Tsr (serine receptor) and Tar (aspartate and maltose receptor).[^7] Each trimer of dimers can be formed with different types of MCPs. Binding with ligands changes the conformation of the receptor dimer. Each receptor dimer within the trimer impacts the activity differently because of sterics.
 - MCPs, CheA (dimer with 5 subunits), and CheW forms receptor arrays. The receptor arrays generally have 2 states: 1) an ordered, dense state, in which CheA activity is higher; 2) a disordered, relaxed state, in which CheA activity is lower.[^4] A visualization of the arrays from [^8] is shown below (we will talk about methylation later.).
 ![image-center](../assets/images/chemotaxis_intro_tod.png){: .align-center}

**CheA**. CheA is composed of 5 domains, in which P3 holds CheA dimers together, P5 binds to MCPs and CheW, P4 is responsible to ATP-dependent autophosphorylation, P2 binds to downstream proteins CheY and CheB, and P1 phosphorylates **CheY** and **CheB** [^4].
 - CheA + ATP -> CheA-P + ADP
 - CheA-P + CheY -> CheY-P
 - CheA-P + CheB -> CheB-P

**CheY**. CheY is phosphorylated by CheA. Upon interacting with FliM in the basal body of flagellum, phosphorylated CheY induces the direction change of flagellum rotation from CCW to CW. As we mentioned before, switching to CW rotations leads to tumbling. CheY dephosphorylation is cataylzed by **CheZ**.
 - CheY-P + CheZ -> CheY + CheZ + P

**CheB**. CheB is phosphorylated by CheA. CheB is responsible for MCP methylation, which we will discuss later. CheB readily autodephosphorylates.
 - CheB-P -> CheB + P

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

*If one E. coli in glucose solution swam from *A concentration to 10A concentration (assume it happened instantaneously), and another stays in a well-mixed glucose with a concentration of 10A, should they have the same tumbling frequency?*
 - No. The first one sensed a *change* in concentration, which indicates that if it keeps swimming in this direction, it might enter an area with higher concentration, so it should decrease tumbling frequency.
 - The cell should decide tumbling frequency based on the *change*, not the absolute concentration.

To achieve these, the cells should be able to record current concentration. This is achieved by **methylation states** (we will explain in more details in the tutorial). The rate of CheA autophosphorylation, besides MCP-ligand binding, is also dependent on **MCP methylation states**. Each MCP monomer has 4 methylation sites. Methylation reduces the negative charge on the receptors, making the receptor array packing more stable, thus increasing CheA autophosphorylation activities. When MCP has a higher methylation state, the rate of CheA autophosphorylation becomes higher.

Recall that CheB is methylated by phosphorylated CheA and is responsible for MCP methylation. When the cell first senses more ligand binding, the higher CheA phosphorylation would lead to more phosphorylated CheB, which then methylates MCPs. MCP records this sensed high concentration via high methylation state.

Therefore, when a cell reaches a region with higher attranctant concentration, initially CW rotation drops by the sensation mechanism, but then the higher CheB phosphorylation makes MCP methylation states higher, thus compensating for the increased binding and restoring tumbling frequencies.

The control of the 4 methylation sites are important to the precise adaptation mechanism [^11], but we will model a simpler version.

[Visit Adaptation Tutoiral](tutorial_adap){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

## Gradient

But instead of the sudden changes we modeled above, the cells swim from a low concentration place to a high concentration place.

[Visit Traveling Up Gradient Tutoiral](tutorial_gradient){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

We've simulated that, when traveling up the gradient, the cells demonstrated a decrease in tumbling frequency until all receptors are saturated. Then the tumbling frequency is restored to the original, by a balance of incrased ligand-receptor binding, and increased methylation states.

But what will happen if the ligands are then removed?
 - How would tumbling frequency change?
 - How would methylation states change?

[Visit Ligand Removal Tutoiral](tutorial_removal){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


## Additional Resources

Some resources/reads if you are interested in the chemotaxis biology:
 - Amazing introduction to chemotaxis: Parkinson Lab [website](http://chemotaxis.biology.utah.edu/Parkinson_Lab/projects/ecolichemotaxis/ecolichemotaxis.html).
 - A good overview: by Webre et al. published in 2003. [Available online](https://www.cell.com/current-biology/pdf/S0960-9822(02)01424-0.pdf)
 - Details on chemotaxis pathway and MCPs: review article by Baker et al. published in 2005 [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/).
 - Details on MCPs: more recent review by Parkinson et al. published in 2015. [Available online](https://www.sciencedirect.com/science/article/abs/pii/S0966842X15000578).
 - Modeling robustness and integral feedback: lecture note by Berg in 2008. [Available online](https://www.weizmann.ac.il/mcb/UriAlon/sites/mcb.UriAlon/files/uploads/lecture_notes_-_robustness_in_bacterial_chemotaxis_.pdf).

[^1]: Randall Munroe. What If? [Available online](https://what-if.xkcd.com/)

[^2]: Pierucci O. 1978. Dimensions of *Escherichia coli* at various growth rates: Model of envelope growth. Journal of Bacteriology 135(2):559-574. [Available online](https://jb.asm.org/content/jb/135/2/559.full.pdf)

[^3]: Sim M, Koirala S, Picton D, Strahl H, Hoskisson PA, Rao CV, Gillespie CS, Aldridge PD. 2017. Growth rate control of flaggelar assembly in *Escherichia coli* strain RP437. Scientific Reports 7:41189. [Available online](https://www.nature.com/articles/srep41189#:~:text=Escherichia%20coli%20is%20a%20prominent,distributed%20across%20the%20cell%20surface.)

[^4]: Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)

[^5]: Weis RM, Koshland DE. 1990. Chemotaxis in *Escherichia coli* proceeds efficiently from different initial tumble frequencies. Journal of Bacteriology 172:2. [Available online](https://jb.asm.org/content/jb/172/2/1099.full.pdf)

[^6]: Berg HC. 2000. Motile behavior of bacteria. Physics today 53(1):24. [Available online](https://physicstoday.scitation.org/doi/pdf/10.1063/1.882934)

[^7]: Achouri S, Wright JA, Evans L, Macleod C, Fraser G, Cicuta P, Bryant CE. 2015. The frequency and duration of *Salmonella* macrophage adhesion events determines infection efficiency. Philosophical transactions B 370(1661). [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4275903/)

[^8]: Turner L, Ping L, Neubauer M, Berg HC. 2016. Visualizing flagella while tracking bacteria. Biophysical Journal 111(3):63--639.

[^9]: Parkinson JS, Hazelbauer, Falke JJ. 2015. Signaling and sensory adaptation in *Escherichia coli* chemoreceptors: 2015 update. [Available online](https://www.sciencedirect.com/science/article/abs/pii/S0966842X15000578)

[^10]: Yang W, Cassidy CK, Ames P, Diebolder CA, Schulten K, Luthey-Schulten Z, Parkinson JS, Briegel A. 2019. *In situ* confomraitonal changes of the *Escherichia coli* serine chemoreceptor in different signaling states. mBio. [Available online](https://mbio.asm.org/content/10/4/e00973-19/article-info)

[^11]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2001. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[Previous](#){: .btn .btn--primary .btn--x-large} [Next Page](tutorial_lr){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
