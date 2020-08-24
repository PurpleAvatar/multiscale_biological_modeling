---
permalink: /chemotaxis/home_walk
title: "Runs and Tumbles"
sidebar:
 nav: "chemotaxis"
---

## *E. coli* explores its world via a random walk

An *E. coli* cell has between five and twelve flagella distributed on its surface.[^Sim2017] Each flagellum can rotate both clockwise and counter-clockwise. When all of the flagella are rotating counter-clockwise, they form a bundle and propel the cell forward at an impressive speed of about 20 µm per second (i.e., about ten times the length of the cell per second). When any flagellum rotates clockwise, the flagella become uncoordinated, and the bacterium winds up rotating in place.[^Baker2005]

When we look at the bacterium's movement, it alternates between periods of "running" in a straight line and then "tumbling" in place (see figure below). When we examine the cell's movement over time, what we see is a *random walk* through its environment. Note that this **run and tumble** view of *E. coli* movement is not dissimilar from the exploration approach taken by our Lost Immortals in the introduction. Recall also from the [prologue](prologue) that an object moving via a random walk will typically travel surprisingly far from its starting point.

![image-center](../assets/images/chemotaxis_intro_runtumble.png){: .align-center}
<figcaption>The run and tumble mechanism of bacterial movement produces a random walk. Image from <a href="http://chemotaxis.biology.utah.edu/Parkinson_Lab/projects/ecolichemotaxis/ecolichemotaxis.html">Parkinson Lab</a>.</figcaption>

* Shuanger: Please crop this figure to avoid the part on the right, which isn't important. I have adjusted the caption. Provide hyperlink in Parkinson lab.

## Tumbling frequency is constant across species

In the absence of an attractant or repellent, *E. coli* stops to tumble once about every 1 to 1.5 seconds.[^Weis1990][^Berg2000] And it is not alone in this behavior; *Salmonella* bacteria (enteric) tumbles about once per second[^Achouri2015], *Enterococcus sacchrolyticus* (enteric) tumbles about once per 1.2 seconds, *Bacillus subtilis*（soil and enteric) tumbles about every 2 seconds[^Turner2016], and *Rhizobia* (soil) tumbles about every 1-2 seconds[^Gotz1987]. Researchers have investigated why different bacteria have different tumbling frequencies,[^Rashid2019][^Mitchell2005] but a definitive explanation for the variation in these frequencies has not been proposed.

Bacteria are amazingly diverse. They have evolved for over three billion years to thrive in practically every environment on the planet, including hazardous human-made environments. They can produce compounds like antibiotics that larger organisms cannot produce. Some eukaryotes are even completely dependent upon bacteria to perform some critical task for them, from digesting their food, to camouflaging them from predators, to helping them develop organs.

* Shuanger: please cite *I Contain Multitudes* by Ed Yong at end of previous paragraph.

And yet despite the diversity present within the bacterial kingdom, the variations in known bacterial tumbling frequencies are not very large. Is there some reason why, regardless of the species, a bacterium's tumbling frequency tends to hover at around 1 tumble per second?

We will return to this question at the close of the module; in the meantime, we will explore the biochemical basis of chemotaxis and see how a bacterium is able to sense an attractant and then adjusts its run and tumble behavior in response. More importantly, we will see that despite bacteria being simple organisms, the reality of how they implement chemotaxis is far more sophisticated than we might ever imagine.

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

[^Gotz1987]: Gotz R and Schmitt R. 1987. *Rhizobium meliloti* swims by unidirectional, intermittent rotation of right-handed flagellar helices. J Bacteriol 169: 3146–3150. [Avaialbe online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC212363/)

[^Lim2019]: Lim S, Guo XK, Boedicker JQ. 2019. Connecting single-cell properties to collective behavior in multiple wild isolates of the *Enterobacter cloacae* complex. PLoS ONE 14(4): e0214719. [Avaialbe online](https://doi.org/10.1371/journal.pone.0214719)

[^Rashid2019]: Rashid S, Long Z, Singh S, Kohram M, Vashistha H, Navlakha S, Salman H, Oltvai ZH, Bar-Joseph Z. 2019. Adjustment in tumbling rates improves bacterial chemotaxis on obstacle-laden terrains. PNAS 116(24):11770-11775. [Available online](https://www.pnas.org/content/116/24/11770)

[^Mitchell2005]: Mitchell JG, Kogure K. 2005. Bacterial motility: links to the environment and a driving force for microbial physics. FEMS Microbiol Ecol 55(2006):3–16. [Available online](https://academic.oup.com/femsec/article/55/1/3/554107)

[Next lesson](home_signal){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
