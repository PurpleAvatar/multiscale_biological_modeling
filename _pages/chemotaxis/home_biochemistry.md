---
permalink: /chemotaxis/home_biochem
title: "A Biochemically Accurate Model of Chemotaxis"
sidebar:
 nav: "chemotaxis"
---

## Transducing a signal to a cell's interior

In the previous lesson, we discussed how a cell recognizes an extracellular signal by receptor proteins on the cell's surface bonding to ligands. Our question now is how the cell conveys this signal to the cell's interior to produce an action via "signal transduction". For example, if *E. coli* senses an increase in the concentration of glucose, meaning that more ligand-receptor bonding is taking place at the receptor that recognizes glucose, how is *E. coli* able to process this information into a change in its behavior?

The engine of signal transduction is a series of **phosphorylation** events. Phosphorylation is a chemical reaction that attaches a phosphoryl group (PO<sub>3</sub><sup>-</sup>) to an organic molecule. (The removal of a phosphoryl group is called **dephosphorylation**.) Phosphoryl modifications serve as an information exchange of sorts because they activate or deactivate certain enzymes. The phosphoryl group usually comes from an adenosine triphosphate (**ATP**) molecule, which is the energy currency of cells, or an upstream phosphorylated molecule.

In the case of chemotaxis, a sequence of phosphorylation events inside *E. coli* called a **phosphorylation cascade** serves to transmit information within the cell about the amount of ligand bonding being detected on the exterior of the cell. In what follows, we discuss the details of how this cascade of chemical reactions leads to a change in bacterial movement.

## Chemotaxis pathway

The transduction pathway for chemotaxis is shown in the figure below. The cell membrane contains receptors called **methyl-acceptring chemotaxis proteins (MCPs)**.  The MCPs, which bridge the cellular membrane, bond to ligand stimuli in the cell exterior, and then bond to other proteins on the inside of the cell. The pathway includes a number of additional proteins, which all start with the prefix *Che* (which is short for "chemotaxis").

On the interior of the cellular membrane, MCPs form complexes with two proteins called **CheW** and **CheA**. In the absence of an attractant concentration, no ligands are bound to an MCP, and so the MCP will freely form complexes with CheW and CheA.

![image-center](../assets/images/chemotaxisphosnew.png){: .align-center}
<figcaption>A summary of chemotaxis pathway. Signal is ligand binding, and the signal is propagated through CheA and CheY phosphorylation, which leads to the response of CW flagellar rotation. Blue curved arrow: phosphorylation; grey curved arrow: dephosphorylation; blue dotted arrow: interaction. Image modified from <a href="http://chemotaxis.biology.utah.edu/Parkinson_Lab/projects/ecolichemotaxis/ecolichemotaxis.html">Parkinson Lab</a>'s illustrations.</figcaption>

When bound to the complex, the CheA molecule **autophosphorylates**, meaning that it is able to add a phosphoryl group to itself --- a concept that might seem mystical if you have not already followed our discussion of autoregulation in the [previous module](motifs/nar). The phosphoryl group comes from ATP, the cellular energy currency we introduced earlier. When an MCP receptor is not bound to the attractant ligand, the complex is more stable and autophosphorylation is faster. Once CheA is phosphorylated, it can then in turn phosphorylate a molecule called **CheY**.
 - CheA + ATP -> CheA-P + ADP
 - CheA-P + CheY -> CheY-P

Phosphorylated CheY will then interact with the flagellum. Specifically, each flagellum has a protein complex called the **flagellar motor switch** that is responsible for controlling the direction of flagellar rotation. The interaction of this protein complex with phosphorylated CheY induces a direction change of flagellar rotation from counter-clockwise to clockwise. As we discussed earlier in this module, this change in flagellar rotation leads to a high background tumbling frequency of every 1 to 1.5 seconds.

As a reminder, this sequence of events is what takes place in the absence of ligand binding, when the *E. coli* cell tumbles frequently. However, when a ligand binds to the MCP, the MCP undergoes conformation changes, which influences the stability of the complex with CheW and CheA. As a result, CheA is less readily able to autophosphorylate, which means that it does not phosphorylate CheY, and so because there is less phosphorylated CheY, the tumbling frequency decreases.

When MCP receptors instead bind to repellent ligands, the situation is reversed. CheA autophosphorylation increases, which increases the rate of phosphorylation of CheY, which increases tumbling frequency.

However, if CheY proteins were to remain phosphorylated in the presence of a repellent, then *E. coli* would tumble forever. We need a reaction that will lower the phosphorylation of CheY, so that CheY can automatically return to a normal unphosphorylated state. The dephosphorylation of CheY is catalyzed by an enzyme called **CheZ**.
 - CheY-P + CheZ -> CheY + CheZ + P

## Adding phosphorylation events to our model of chemotaxis

We would like to simulate the reactions driving chemotaxis signal transduction and see what happens if the bacterium "senses an attractant", meaning that the attractant ligand's concentration increases and leads to more receptor-ligand binding. To do so, we will build on the model for ligand-receptor dynamics that we introduced in the previous lesson.

Specifically, once we add the reactions that occur in the interior of the cell to our model, we would like to see what happens as we change the concentrations of the ligand. Ideally, this system should help the bacterium distinguish between different ligand concentrations. That is, the higher the concentration of an attractant ligand, the lower the concentration of phosphorylated CheY, and thus the lower the tumbling frequency of the bacterium.

But does higher attractant concentration lead to a lower concentration of CheY? Let's see by incorporating the phosphorylation pathway into our BNG simulation in the following tutorial.

[Visit Phosphorylation Tutorial](tutorial_phos){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Tumbling frequency and changing ligand concentrations

When no ligand is added, we see the concentrations remain at steady state. CheY activity remains at the background level, resulting in background tumbling frequency.

![image-center](../assets/images/chemotaxis_tutorial5.png){: .align-center}

When we have 5000 attractant molecules, the addition of attractant molecules increases the concentration of bound receptors, therefore leads to less CheA autophosphorylation, and less CheY activities.

![image-center](../assets/images/chemotaxis_tutorial6.png){: .align-center}

If we have 1e5 attractant molecules, the higher concentration of ligands further decreases the steady state CheY activities.

![image-center](../assets/images/chemotaxis_tutorial7.png){: .align-center}

With the addition of attractants, more receptor complexes are bound to attractants, and therefore less CheA autophosphorylation happens (here we include the CheA as part of the receptor complex). As a result, less CheY can be phosphorylated by CheA, and therefore, CheY phosphorylates the flagellar proteins less frequently, reducing tumbling frequency. And a higher attractant concentration leads to more decrease in tumbling frequency (before receptors are saturated and can no longer have higher bound receptor concentration).

When we add 5000 repellent molecules, the resulted higher concentration of bound receptors leads to higher CheA autophosphorylation, and therefore higher CheY activities.

![image-center](../assets/images/chemotaxis_tutorial_phosrepel5e3.png){: .align-center}

When we add 1e5 repellent molecules, the higher ligand-receptor binding leads to a further increase phosphorylated CheA and phosphorylated CheY.

![image-center](../assets/images/chemotaxis_tutorial_phosrepel1e5.png){: .align-center}

The ability to detect different ligand concentrations over many different types of ligands and change behavior in a response that is commensurate with the concentration of the ligand is a remarkable feature of bacteria like *E. coli*. But what we have shown in this lesson is just half of the story. In the next lesson, we will see that the biochemical realities of chemotaxis are even more complicated, and for good reason -- this complexity will allow *E. coli* to react surprisingly "intelligently" to an ever-changing environment.

[^Munroe]: Randall Munroe. What If? [Available online](https://what-if.xkcd.com/)

[^Pierucci1978]: Pierucci O. 1978. Dimensions of *Escherichia coli* at various growth rates: Model of envelope growth. Journal of Bacteriology 135(2):559-574. [Available online](https://jb.asm.org/content/jb/135/2/559.full.pdf)

[^Sim2017]: Sim M, Koirala S, Picton D, Strahl H, Hoskisson PA, Rao CV, Gillespie CS, Aldridge PD. 2017. Growth rate control of flagellar assembly in *Escherichia coli* strain RP437. Scientific Reports 7:41189. [Available online](https://www.nature.com/articles/srep41189#:~:text=Escherichia%20coli%20is%20a%20prominent,distributed%20across%20the%20cell%20surface.)

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

[^Bertoli2013]: Bertoli C, Skotheim JM, de Bruin RAM. 2013. Control of cell cycle transcription during G1 and S phase. Nature Reviews Molecular Cell Biology 14:518-528. [Available online](https://www.nature.com/articles/nrm3629).

[^Li2004]: Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^Stock1991]: Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^Spiro1997]: Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).

[Next Page: Adaptation](home_senseadap){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
