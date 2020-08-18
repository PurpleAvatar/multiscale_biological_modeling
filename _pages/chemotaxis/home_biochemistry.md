---
permalink: /chemotaxis/home_biochem
title: "Biochemistry and Modeling"
sidebar:
 nav: "chemotaxis"
---

## More on Signal transduction pathway - phosphorylation

Let's get back to our signal transduction pathway which includes 1) an external stimuli, 2) a series of molecular events, 3) a resulted cellular response. We got how the stimuli is generated. We will get into more cellular details into the molecular events and response.

The series of molecular events are a series of phosphorylation events.

What's phosphorylation and why so many phosphorylation reactions? **Phosphorylation** is a chemical reaction that attaches a phosphoryl group (PO<sub>3</sub><sup>-</sup>) to an organic molecule. The removal of the phosphoryl group is dephosphorylation. Such modifications can activate or deactivate certain enzymes like switches. For example, a cyclin dependent kinase, when activated by G1/S cyclin, can phosphorylate its target proteins to activate DNA replication and initiate S phase[^Bertoli2013].

In chemotaxis, the direction of flagellar rotation is also controlled by phosphorylation pathways. After ligand-receptor binding, the phosphorylation events transduce the signal to the flagelli. The sequence of phosphorylation event is called a phosphorylation cascade. 

## Chemotaxis pathway

This pathway includes the receptor we've discussed - receptor complex MCP, a series of chemotaxis proteins - CheW, CheA, CheY, CheZ (*Che* stands for chemotaxis), and the basal body of flagelli. The figure provides a visualization[^ParkinsonLab].
![image-center](../assets/images/chemotaxisphosnew.png){: .align-center}
<figcaption>A summary of chemotaxis pathway. Signal is ligand binding, and the signal is propagated through CheA and CheY phosphorylation, which leads to the response of CW flagllar rotation.</figcaption>

Introduction to the pathway:

**MCPs**. On the cell membrane, there are receptors called **methyl-acceptring chemotaxis proteins (MCPs)**. They form complexes with **CheW** and **CheA**.

**CheA**. CheA undergoes autophosphorylation. It can then phosphorylates CheY.
 - CheA + ATP -> CheA-P + ADP
 - CheA-P + CheY -> CheY-P

**CheY**. CheY is phosphorylated by CheA. Upon interacting with FliM in the basal body of flagellum, phosphorylated CheY induces the direction change of flagellum rotation from CCW to CW. As we mentioned before, switching to CW rotations leads to tumbling. CheY dephosphorylation is cataylzed by **CheZ**.
 - CheY-P + CheZ -> CheY + CheZ + P

**CheZ**. CheZ dephosphorylates CheY, as introduced above.


When the cell is in an environment with no ligand, CheA autophosphorylation occurs at a background frequency, leading to a CheY phosphorylation rate that would maintain the background tumbling frequency of every 1-1.5s.

When the receptors bind to attractant molecules, CheA autophosphorylation lowers, decreasing tumbling frequency. When the receptors bind to repellent molecules, CheA autophosphorylation increasess, increasing tumbling frequency.

## Modeling phosphorylation events



[Visit Ligand-Receptor Dynamics Tutoiral](tutorial_phos){: .btn .btn--primary .btn--large}
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

[^Bertoli2013]: Bertoli C, Skotheim JM, de Bruin RAM. 2013. Control of cell cycle transcription during G1 and S phase. Nature Reviews Molecular Cell Biology 14:518-528. [Available online](https://www.nature.com/articles/nrm3629).

[^Li2004]: Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^Stock1991]: Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^Spiro1997]: Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).

[Next Page: Sensation and Adaptation](home_senseadap){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}