---
permalink: /chemotaxis/home_signal
title: "Signaling and Ligand-Receptor Dynamics"
sidebar:
 nav: "chemotaxis"
---

## Signaling Pathway

A key characteristic of living organisms is the ability to respond to stimuli in the environment. Chemotaxis is one of those behaviors. It relies on the ability to perceive a change (ligand concentration), and react accordingly (adjust direction of movement). This is an example of *signal transduction pathway*, which includes 1) an external stimuli, 2) a series of molecular events, 3) a resulted cellular response. 

Why are we interested in signaling pathways? Recall the discussion on gene expression regulation in the Motif Module. An external signal can lead to change in gene expression (response). Such mechanisms provides stability to biological systems when there is perturbation in the enviornment. Internal temperature and ion concentrations, etc. of organisms need to be maintained when there is a signal of temperature/concentration change to keep enzymes functional. Besides fitness of an individual, singaling also enables a group of organisms to have higher fitness, for example, biofilm formation and mate-finding. We didn't include cellular details for gene expression regulation, but to understand chemotaxis, we will need to include cellular details.

In the case of chemotaxis, the stimuli is ligand binding; the cell perceives this change, and propagates this information through a series of molecules, which leads to the cellular response of changed flagellar movement.

![image-center](../assets/images/chemotaxis_signal.png){: .align-center}
<figcaption>Signaling pathway for *E. coli* chemotaxis.</figcaption>

We will walk through the details of the pathway, and build a model step by step.


## Modeling Ligand-Receptor dynamics

We just discussed that ligand-receptor binding is the stimulus. But how is this stimulus generated? How does the envrionmental concentration of the ligands impact ligand-receptor binding?

We can explore this question with a model of reversible bimolecular reaction. In our system, we have 2 types of molecules, MCPs(T) and ligands(L). T and L can bind to form an intermediate TL, and TL can dissociate. If we give the system an infinite time to react, what will happen?

At the begining of the reaction, TL will be formed quickly at the expense of free T and L. After a while, there will be more TL ready to dissociate, but fewer T and L to form TL. At some point, the rate of TL formation will equal to the rate of TL dissociation. As time progresses, the concentrations will remain constant, so it is called a *steady state*.

In this Module, we will use [BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) to build a set of models to simulate chemotaxis activities. We will start from building a simulation for equilbrium of bimolecular reversible reaction between ligand and receptors.

[Visit Ligand-Receptor Dynamics Tutoiral](tutorial_lr){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

Why BNG instead of CellBlender? We don't care about the spacial distribution of receptor and ligands here - an *E. coli* is small compared to gradients it encounters in real life (no ligand concentration difference across its body - but there are some bacteria that experience different concentration across its body), and we only care about a region the receptors are located at, so we can assume the ligand concentration is uniform everywhere within that region.


## Reversible reactions and steady state of a system

Why do we care that the reaction is reversible? Because for ligand-receptor dynamics, the receptors are generally complex molecules produced by the organism, so should be reusable. The only way that the receptor can binds to ligands repetitively is to release the ligand.

For reversible reactions, the system will reach the steady state we've showed. We can calculate it by hand.

To simply the calculations, assume we have a system with nicer numbers. Our system has 50M free ligand molecules (L, denote with *L<sub>0</sub> = 50*) and 50M free receptor molecules (T, denote with *T<sub>0</sub> = 50*), and the reaction proceeds as following:
- L + T <-> L.T, where *k<sub>bind</sub> = 1* M<sup>-1</sup>s<sup>-1</sup>, *k<sub>dissociate</sub> = 5* s<sup>-1</sup>.(shortened as *k<sub>b</sub>, k<sub>d</sub>*)

Calculation:
- The rate of forward reaction is *k<sub>b</sub>[L][T]*, and the rate of reverse reaction is *k<sub>d</sub>[L.T]*.
- At steady state, rate of forward reaction is equal to the rate of reverse reaction. So *k<sub>b</sub>[L][T] = k<sub>d</sub>[L.T]*. (eq.1)
- Because of conservation of mass, all L.T in our system must formed by L and T. Therefore, at anytime, we have *[L] = L<sub>0</sub> - [L.T]* and *[T] = T<sub>0</sub> - [L.T]*. (eq.2 & 3)
- Substitute eq.2 & 3 into eq.1, we can get *k<sub>b</sub>(L<sub>0</sub> - [L.T])([T] = T<sub>0</sub> - [L.T]) = k<sub>d</sub>[L.T]*. (eq.4)
- Assign *x = [L.T]*. Substitute *L<sub>0</sub> = 50*, *T<sub>0</sub> = 50*, *k<sub>bind</sub> = 1*, and *k<sub>dissociate</sub> = 5* into eq.4, we get *1 (50 - x)(50 - x) = 5 x*. (eq.5)
- So *[L.T] = x = 36.492*.
- Therefore the steady-state concentration of L.T is 36.492 M. Accordingly, the steady-state concentration of L and T is 13.508 M.

What if the forward reaction becomes faster? For example, *k<sub>bind</sub> = 2* M<sup>-1</sup>s<sup>-1</sup>? More L.T should be formed. Let's confirm this by simply change eq.5 to *2 (50 - x)(50 - x) = 5 x*. Solve it, we get *x = 40*. So the steady state concentration for L.T is 40 M, for L and T is 10 M.

What if there are more ligands? For example, *L<sub>0</sub> = 100* M. More L.T should be formed. Similarly, we can change eq.5 to *1 (100 - x)(50 - x) = 5 x*, and we will get steady state concentration for L.T is 45.779 M, for L and T is 4.221 M.

**STOP**: What if backward reaction becomes faster? For example, *k<sub>dissociate</sub> = 10* s<sup>-1</sup>? Confirm your hypothesis by calculation.

Let's get back to the ligand-receptor dynamics for *E. coli*. Change the parameters to *L<sub>0</sub> = 1e4*,  *T<sub>0</sub> = 7000*, *k<sub>b</sub> = 8.8e8/6.02e8, k<sub>d</sub> = 35*. (Excersice for you: what are the units?) We can calculate that the steady state concentration for L.T is about 4794 (Excersice for you: what unit?).

Here we've showed that using BNG and calculating by hand reach the same conclusion for bimolecular reactions.

But if we can calculate this by hand, why do we still need BNG? The benefit of BNG is that, when we have more reactions involved in the system, calculating (or even setting up all the equations) by hand is no longer possible. We will introduce more complexity in the pathway through the module.



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

[Next Page: Chemotaxis pathway](home_biochem){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}