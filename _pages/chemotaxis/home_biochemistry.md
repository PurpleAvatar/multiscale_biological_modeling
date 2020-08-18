---
permalink: /chemotaxis/home_biochem
title: "Biochemistry and Modeling"
sidebar:
 nav: "chemotaxis"
---

## Signaling Pathway

A key characteristic of living organisms is the ability to respond to stimuli in the environment. Chemotaxis is one of those behaviors. It relies on the ability to perceive a change (ligand concentration), and react accordingly (adjust direction of movement). This is an example of *signal transduction pathway*, which includes 1) an external stimuli, 2) a series of molecular events, 3) a resulted cellular response. 

Why are we interested in signaling pathways? Recall the discussion on gene expression regulation in the Motif Module. An external signal can lead to change in gene expression through transcription factors. We didn't include cellular details there. But in this module, we will get into cellular details to understand chemotaxis behaviors.

In the case of chemotaxis, the stimuli is ligand binding; the cell perceives this change, and propagates this information through a series of molecules, which leads to the cellular response of changed flagellar movement.

This pathway includes a receptor complex MCP, a series of chemotaxis proteins - CheW, CheA, CheY, CheZ (*Che* stands for chemotaxis), and the basal body of flagelli. The figure provides a visualization.
![image-center](../assets/images/chemotaxisphosnew.png){: .align-center}
<figcaption>A summary of chemotaxis pathway. Signal is ligand binding, and the signal is propagated through CheA and CheY phosphorylation, which leads to the response of CW flagllar rotation.</figcaption>

Introduction to the pathway:

**MCPs**. On the cell membrane, there are receptors called **methyl-acceptring chemotaxis proteins (MCPs)**. They form complexes with **CheW** and **CheA**.

**CheA**. CheA undergoes autophosphorylation. It can then phosphorylates CheY.
 - CheA + ATP -> CheA-P + ADP
 - CheA-P + CheY -> CheY-P
 - CheA-P + CheB -> CheB-P

**CheY**. CheY is phosphorylated by CheA. Upon interacting with FliM in the basal body of flagellum, phosphorylated CheY induces the direction change of flagellum rotation from CCW to CW. As we mentioned before, switching to CW rotations leads to tumbling. CheY dephosphorylation is cataylzed by **CheZ**.
 - CheY-P + CheZ -> CheY + CheZ + P

**CheZ**. CheZ dephosphorylates CheY, as introduced above.


When the cell is in an environment with no ligand, CheA autophosphorylation occurs at a background frequency, leading to a CheY phosphorylation rate that would maintain the background tumbling frequency of every 1-1.5s.

When the receptors bind to attractant molecules, CheA autophosphorylation lowers, decreasing tumbling frequency. When the receptors bind to repellent molecules, CheA autophosphorylation increasess, increasing tumbling frequency.


## Modeling Ligand-Receptor dynamics

We just discussed that ligand-receptor binding is the stimulus. But how is this stimulus generated? How does the envrionmental concentration of the ligands impact ligand-receptor binding?

We can explore this question with a model of reversible bimolecular reaction. In our system, we have 2 types of molecules, MCPs(T) and ligands(L). T and L can bind to form an intermediate TL, and TL can dissociate. If we give the system an infinite time to react, what will happen?

At the begining of the reaction, TL will be formed quickly at the expense of free T and L. After a while, there will be more TL ready to dissociate, but fewer T and L to form TL. At some point, the rate of TL formation will equal to the rate of TL dissociation. This is call an *equilibrium*.

In this Module, we will use [BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) to build a set of models to simulate chemotaxis activities. We will start from building a simulation for equilbrium of bimolecular reversible reaction between ligand and receptors.


[Visit Ligand-Receptor Dynamics Tutoiral](tutorial_lr){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}



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

[Next Page: Sensation and Adaptation](home_senseadap){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
