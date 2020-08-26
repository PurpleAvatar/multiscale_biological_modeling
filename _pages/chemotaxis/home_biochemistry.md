---
permalink: /chemotaxis/home_biochem
title: "Biochemistry and Modeling"
sidebar:
 nav: "chemotaxis"
---

## Transducing a signal to a cell's interior

In the last lesson, we discussed how a cell recognizes an extracellular signal by receptor proteins on the cell's surface bonding to ligands. Our question now is how the cell conveys this signal to the cell's interior to produce an action via "signal transduction". For example, if *E. coli* senses an increase in the concentration of glucose, meaning that more ligand-receptor bonding is taking place at the receptor that recognizes glucose, how is *E. coli* able to process this information into a change in its behavior?

The engine of signal transduction is a series of **phosphorylation** events. Phosphorylation is a chemical reaction that attaches a phosphoryl group (PO<sub>3</sub><sup>-</sup>) to an organic molecule. (The removal of a phosphoryl group is called **dephosphorylation**.) Phosphoryl modifications serve as an information exchange of sorts because they activate or deactivate certain enzymes. For example, a cyclin dependent kinase, when activated by G1/S cyclin, can phosphorylate its target proteins to activate DNA replication and initiate S phase[^Bertoli2013].

* SHUANGER: Do you feel strongly about keeping cyclin? IMO it is clear without it and doesn't add much.

In the case of chemotaxis, after ligand-receptor binding has been detected, a sequence of phosphorylation events inside *E. coli* called a **phosphorylation cascade** serves to convey the extracellular signal to the flagella. In what follows, we discuss the details of how this cascade of chemical reactions leads to a change in bacterial movement.

## Chemotaxis pathway

The transduction pathway for chemotaxis is shown in the figure below. The cell membrane contains receptors called **methyl-acceptring chemotaxis proteins (MCPs)**.  The MCPs, which bridge the cellular membrane, bond to ligand stimuli in the cell exterior, and then bond to other proteins on the inside of the cell to convey that the signal has been detected. The pathway includes a number of additional proteins, which all start with the prefix *Che* (which stands for "chemotaxis")

* SHUANGER: It is not clear at this time how the bonding of the ligand causes a change w/r/t forming a complex with CheW and CheA. This needs to be crystal clear.

![image-center](../assets/images/chemotaxisphosnew.png){: .align-center}
<figcaption>A summary of chemotaxis pathway. Signal is ligand binding, and the signal is propagated through CheA and CheY phosphorylation, which leads to the response of CW flagellar rotation. Blue curved arrow: phosphorylation; grey curved arrow: dephosphorylation; blue dotted arrow: interaction.</figcaption>

* SHUANGER: cite [^ParkinsonLab] in the figure caption above.

The **CheA** molecule **autophosphorylates**, meaning that it is able to add a phosphoryl group to itself --- a concept that might seem mystical if you have not already followed our discussion of autoregulation in the [previous module](motifs/nar). When an MCP receptor is not bound to the attractant ligand, autophosphorylation is faster. Once CheA is phosphorylated, it can then in turn phosphorylate a molecule called **CheY**.
 - CheA + ATP -> CheA-P + ADP
 - CheA-P + CheY -> CheY-P

* SHUANGER: These equations are going to come out of left field a bit. The fact that ATP is a critical substance for the cell to use in the phosphorylation process is important I think.

* SHUANGER: you previously had "MCPs form complexes with **CheW** and **CheA**." But what is the point of CheW?  It has gotten lost in the shuffle here.

Upon interacting with FliM in the basal body of flagella, phosphorylated CheY induces a direction change of flagellar rotation from counter-clockwise to clockwise. As we have said previously, the change in flagellar rotation leads to an increased tumbling frequency.

* SHUANGER: define FliM

In an environment that lacks ligand, CheA autophosphorylation occurs at a background frequency, leading to a CheY phosphorylation rate that would maintain the background tumbling frequency of every 1-1.5s. But when the MCP receptors bind to attractant molecules, CheA autophosphorylation lowers. In turn, there is less phosphorylated CheA, which means that the rate of phosphorylation of CheY decreases as well, decreasing the frequency of tumbles.

When receptors bind to repellent ligands, the situation is reversed. CheA autophosphorylation increases, which increases the rate of phosphorylation of CheY, which increases tumbling frequency.

Finally, say that a repellent is detected and the rate of CheY phosphorylation increases. If these CheY proteins were to remain phosphorylated, then *E. coli* would tumble forever. We need a reaction that will lower the phosphorylation of CheY, so that if the phosphorylation rate of CheY slows, then CheY can automatically return to a normal unphosphorylated state. The dephosphorylation of CheY is catalyzed by an enzyme called **CheZ**.
 - CheY-P + CheZ -> CheY + CheZ + P

## Adding phosphorylation events to our model of chemotaxis

We would like to simulate the reactions driving chemotaxis signal transduction and see what happens if the bacterium "senses an attractant", meaning that the attractant ligand's concentration increases and leads to more receptor-ligand binding. To do so, we will build on the model for ligand-receptor dynamics that we introduced in the previous lesson.

Specifically, once we add the reactions that occur in the interior of the cell to our model, we would like to see what happens as we change the concentrations of the ligand. Ideally, this system should help the bacterium distinguish between different ligand concentrations. That is, the higher the concentration of an attractant ligand, the lower the concentration of phosphorylated CheY, and thus the lower the tumbling frequency of the bacterium.

But does higher attractant concentration lead to a lower concentration of CheY? Let's see by incorporating the phosphorylation pathway into our BNG simulation in the following tutorial.

[Visit Phosphorylation Tutorial](tutorial_phos){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## *E. coli* can detect changing ligand concentrations

When no ligand is added, we see the concentrations remain at steady state. CheY activity remains at the background level, resulting in background tumbling frequency.

![image-center](../assets/images/chemotaxis_tutorial5.png){: .align-center}

If we have 1e4 attractant molecules.

![image-center](../assets/images/chemotaxis_tutorial6.png){: .align-center}

If we have 1e5 attractant molecules.

![image-center](../assets/images/chemotaxis_tutorial7.png){: .align-center}

With the addition of attractants, more receptor complexes are bound to attractants, and therefore less CheA autophosphorylation happens (here we include the CheA as part of the receptor complex). As a result, less CheY can be phosphorylated by CheA, and therefore, CheY phosphorylates the flagellar proteins less frequently, reducing tumbling frequency. And a higher attractant concentration leads to more decrease in tumbling frequency (before receptors are saturated and can no longer have higher bound receptor concentration).

But this is only half of the story. In the next section, we will code up the adaptation, including CheR, CheB, and methylation states for chemotaxis.



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
