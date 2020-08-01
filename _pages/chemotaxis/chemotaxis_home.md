---
permalink: /chemotaxis/home
title: "Introduction to Chemotaxis"
sidebar: 
 nav: "chemotaxis"
---

### Prologue

**"Lost Immortals" in *What if*.**


### Introductino to Chemotaxis

*Escherichia coli* (also *E. coli*) is a rod-shaped bacterium commonly found in the lower intestine of endotherms. Being commensal at the most of the time, it is, paradoxically, one of the main pathogens responsible for intraintestinal and extraintestinal infections.[^1] It is also *the most* widely studied prokaryotic model organism. They are small, like other prokaryotes are, with a length about 2um, and a diameter 0.25-1um.[^2] **The small size of *E. coli* puts them into a similar situation like the lost explorers are: how to explore the space efficiently to find food?**

The behavior of cells moving towards/away from a stimulus is called **chemotaxis**. For *E. coli*, moving towards attractants (ex. glucose, electron acceptros), and moving away from repellents (ex. Ni2+, Co2+) are all considered chemotaxis behaviors.

Here is a cute video of *E. coli* moving towards a sugar crystal.
<iframe width="640" height="360" src="https://www.youtube.com/embed/F6QMU3KD7zw" frameborder="0" allowfullscreen></iframe>

### How does *E. coli* know where to go?

*E. coli* has 5-12 flagelli randomly distributed in the surface.[^3] Each flagelum rotates clockwise (CW) or counter-clockwise (CCW). That leads to two states of movement: 1) when flagelli rotates in CCW, they form a bundle, and propells the cells to swiming smoothly at speeds of 20 um per second, called **run**; 2) when some flaggeli in the bundle rotates CW, the flagelli become uncoordinated and reorients with a much slower net movement speed in place, called **tumble**.[^4] 

![image-center](../assets/images/chemotaxis_intro_runtumble.png){: .align-center}
(Image from Parkinson Lab, University of Utah)

In a uniform environment, *E. coli* tumbles once about every 1-1.5 seconds.[^5][^6] Such tumbling frequency is clever, because if the bacteria tumble too much, it won't be able to explore the space; but if tumble too little, it might go too far in the wrong direction.

**Insert demonstration of different tumbling frequency?**

*E. coli* determines if it is in the right direction by comparing the concentration of ligand/receptor with the concentration *in the past*. If the cell senses a higher attractant concentration, it tumbles less; if it senses a lower attractant concentration, it tumbles more. Moreover, although it is still under active research, the cell tends to rotate at a smaller angle when traveling up the attractant gradient compared to traveling down the gradient.[^7] For repellent, it is the opposite. So the net effect is that the cell moves towards high concentration of attractants, and away from high concentration of repellents.

**Insert demonstration?**

### The chemistry

*E. coli* compares the current vs. past concentration of ligand and then controls the direction of flagellar rotation accordingly. This is achieved by a signaling pathway summarized in the figure.
![image-center](../assets/images/chemotaxispathway.png){: .align-center}
(Image from Parkinson Lab, University of Utah)

A summary of the pathway:
 - On the cell membranes, there are receptors called methyl-acceptring chemotaxis proteins (MCPs). They form complexes with CheW and CheA (*Che* stands for chemotaxis). There are methylation sites on CheR.
 - CheA autophosphorylates itself, which then phosphorylates CheY and CheB.
 - Phosphorylated CheY then interacts the basal body of flagellum, triggering CW rotation.
 - CheY is dephosphorylated by CheZ.
 - Phosphorylated CheB demethylates MCP.
 - CheR methylates MCP.
 - The ***sensation*** part: the cell needs to detect a gradient. The rate of CheA autophosphorylation is dependent on **MCP-ligand binding**. When MCP binds with attractants, rate of CheA autophosphorylation decreases, and thus CheY activity decrases, and flagellar CW rotation decrases, leading to less tumble. It is the opposite for the repellent.
 - The ***adaptation*** part: the cell should go back to original tumbling frequency when no gradient presents despite what the concentration is. The rate of CheA autophosphorylation is also dependent on **MCP methylation states**. When MCP has a higher methylation state, the rate of CheA autophosphorylation becomes higher. Therefore, when a cell reaches a region with higher attranctant concentration, initially CW rotation drops by the sensation mechanism, but then the higher CheB phosphorylation makes MCP methylation states higher, thus compensating for the increased binding and restoring tumbling frequencies.


In this module, we will build a BioNetGen model to simulate this pathway. It might sounds a bit overwhelming now, but we will do it step by step. Have fun!





[^1] Tenaillon O, Skurnik D, Picard B, Denamur E. 2010. The population genetics of commensal *Escherichia coli*. Nature Reviews Microbiology 8:207-217. [Available online](https://www.nature.com/articles/nrmicro2298)

[^2] Pierucci O. 1978. Dimensions of *Escherichia coli* at various growth rates: Model of envelope growth. Journal of Bacteriology 135(2):559-574. [Available online](https://jb.asm.org/content/jb/135/2/559.full.pdf)

[^3] Sim M, Koirala S, Picton D, Strahl H, Hoskisson PA, Rao CV, Gillespie CS, Aldridge PD. 2017. Growth rate control of flaggelar assembly in *Escherichia coli* strain RP437. Scientific Reports 7:41189. [Available online](https://www.nature.com/articles/srep41189#:~:text=Escherichia%20coli%20is%20a%20prominent,distributed%20across%20the%20cell%20surface.)

[^4] Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)

[^5] Weis RM, Koshland DE. 1990. Chemotaxis in *Escherichia coli* proceeds efficiently from different initial tumble frequencies. Journal of Bacteriology 172:2. [Available online](https://jb.asm.org/content/jb/172/2/1099.full.pdf)

[^6] Berg HC. 2000. Motile behavior of bacteria. Physics today 53(1):24. [Available online](https://physicstoday.scitation.org/doi/pdf/10.1063/1.882934)

[^7] Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2001. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[Previous](#){: .btn .btn--primary .btn--x-large} [Next Page](tutorial_lr){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


