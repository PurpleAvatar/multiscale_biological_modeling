---
permalink: /chemotaxis/home_biochem
title: "Biochemistry and Introduction to Rule-Based Modeling"
sidebar:
 nav: "chemotaxis"
---

## Biochemistry

*E. coli* run and tumble is controlled by a series of chemotaxis proteins. This figure summarizes the signaling pathway.
![image-center](../assets/images/chemotaxispathway.jpg){: .align-center}
<figcaption>Summary of E. coli chemotaxis pathway. Image from Parkinson Lab, University of Utah.</figcaption>

Detailed explanation of the pathway:

**Receptor Complexes**. On the cell membrane, there are receptors called **methyl-acceptring chemotaxis proteins (MCPs)**. They form complexes with **CheW** and **CheA** (*Che* stands for chemotaxis).
 - There are five types of MCPs, Tsr, Tar, Tap, Trg, and Aer, specific for different species of ligand molecules. Most studies focus on the two most abundant types: Tsr (serine receptor) and Tar (aspartate and maltose receptor), and Aer (oxygen receptor) is less well understood.[^Parkinson2015] The MCPs form trimer of dimer structure. A trimer can be a mix of Tsr, Tar, Tap, Trg dimers. Binding with ligands changes the conformation of the receptor dimer. Each receptor dimer within the trimer impacts the activity differently because of sterics.
 - MCPs, CheA (dimer with 5 subunits), and CheW forms receptor arrays. The receptor arrays generally have 2 states: 1) an ordered, dense state, in which CheA activity is higher; 2) a disordered, relaxed state, in which CheA activity is lower.[^Baker2005] A visualization of the arrays from[^Yang2019] is shown below (as in the figure, each MCP has 4 methylation states, but we will talk about methylation later).

 ![image-center](../assets/images/chemotaxis_intro_tod.png){: .align-center}
 <figcaption>MCP array structures. From Yang et al.[^Yang2019]</figcaption>

**CheA**. CheA is composed of 5 domains, in which P3 holds CheA dimers together, P5 binds to MCPs and CheW, P4 is responsible to ATP-dependent autophosphorylation, P2 binds to downstream proteins CheY and CheB, and P1 phosphorylates **CheY** and **CheB** [^Baker2005].
 - CheA + ATP -> CheA-P + ADP
 - CheA-P + CheY -> CheY-P
 - CheA-P + CheB -> CheB-P

**CheY**. CheY is phosphorylated by CheA. Upon interacting with FliM in the basal body of flagellum, phosphorylated CheY induces the direction change of flagellum rotation from CCW to CW. As we mentioned before, switching to CW rotations leads to tumbling. CheY dephosphorylation is cataylzed by **CheZ**.
 - CheY-P + CheZ -> CheY + CheZ + P

**CheB**. CheB is phosphorylated by CheA. CheB is responsible for MCP methylation, which we will discuss later. CheB readily autodephosphorylates.
 - CheB-P -> CheB + P

When the cell is in an environment with no ligand, CheA autophosphorylation occurs at a background frequency, leading to a CheY phosphorylation rate that would maintain the background tumbling frequency of every 1-1.5s.

When the receptors bind to attractant molecules, CheA autophosphorylation lowers, decreasing tumbling frequency. When the receptors bind to repellent molecules, CheA autophosphorylation increasess, increasing tumbling frequency.


## Combinatorial explosion and Rule-based modeling

Consider we want to program a simplified version of part of the pathway above-
 - Serine receptor complex (Tsr), can be bound to not bound to a ligand
 - CheA associated with Tsr, can be phosphorylated or not
 - The state of Tsr binding and CheA phosphorylation will impact downstream reactions, so we would like to specify each of the states

If we have 1 complex, and 1 CheA, we could have the following states:
 - Tsr-bound, CheA-phosphorylated
 - Tsr-bound, CheA-unphosphorylated
 - Tsr-free, CheA-phosphorylated
 - Tsr-free, CheA-unphosphorylated

If we have 2 complexes, and 2 CheA molecules associated, assuming the two are interchangable, we could have the following states:
 - Tsr1-bound, CheA1-phosphorylated, Tsr2-bound, CheA2-phosphorylated
 - Tsr1-bound, CheA1-phosphorylated, Tsr2-bound, CheA2-unphosphorylated
 - Tsr1-bound, CheA1-phosphorylated, Tsr2-free, CheA2-phosphorylated
 - Tsr1-bound, CheA1-phosphorylated, Tsr2-free, CheA2-unphosphorylated
 - Tsr1-bound, CheA1-unphosphorylated, Tsr2-bound, CheA2-unphosphorylated
 - Tsr1-bound, CheA1-unphosphorylated, Tsr2-free, CheA2-phosphorylated
 - Tsr1-bound, CheA1-unphosphorylated, Tsr2-free, CheA2-unphosphorylated
 - Tsr1-free, CheA1-phosphorylated, Tsr2-free, CheA2-unphosphorylated
 - Tsr1-free, CheA1-phosphorylated, Tsr2-free, CheA2-phosphorylated
 - Tsr1-free, CheA1-unphosphorylated, Tsr2-free, CheA2-unphosphorylated

And that number grows quickly when we have more molecules, more reactions, and more states. Similar to modeling other biological systems, this is a classical problem of combinatorial explosion[^Hlavacek2003].

The combinatorial complexity poses two challenges in programming: 1) how to specify those states, 2) how to simulate such a system. 

As we just tried, it's hard to *explicitly* specify the states. However, if we were to model the a downstream reaction between a CheY molecule and (Tsr1+CheA1), the CheY molecule only cares about whether Tsr1 is bound or free and whether CheA1 is phosphorylated or not; Tsr2 and CheA2 doesn't matter. We can specify a rule for reaction between CheY and (Tsr+CheA) regardless the state of the whole system except the molecules we are interested in. Such **rule based modeling** can simplify model construction and computation [^Hlavacek2006].

When computing with rule based modeling, the program starts with an initial condition, and evaluates the rules to modify the state. Two commonly used algorithms are differential equations and stochastic Gillespie algorithm, which we will introduce in the tutorials.

In the later pages, we will build a molecular level simulation of *E. coli* chemotaxis behavior with rule based modeling using [BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409).



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

[Next Page: Sensation and Adaptation](home_senseadap){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
