---
permalink: /chemotaxis/home_walk
title: "Introduction to Chemotaxis"
sidebar:
 nav: "chemotaxis"
---

## How does *E. coli* explore the world?

*E. coli* has 5-12 flagelli randomly distributed in the surface.[^Sim2017] Each flagelum rotates clockwise (CW) or counter-clockwise (CCW). That leads to two states of movement: 1) when flagelli rotates in CCW, they form a bundle, and propel the cells to swiming smoothly at speeds of 20 µm per second, called **run**; 2) when some flaggeli in the bundle rotates CW, the flagelli become uncoordinated and reorients with a much slower net movement speed in place, called **tumble**.[^Baker2005]

![image-center](../assets/images/chemotaxis_intro_runtumble.png){: .align-center}
<figcaption>Run and tumble. Left: relationship between flagellar rotation and run vs. tumble. Right: a run-and-tumble trajectory towards right. Image from Parkinson Lab, University of Utah.</figcaption>

In a uniform environment, *E. coli* tumbles once about every 1-1.5 seconds.[^Weis1990][^Berg2000] Tumbling frequency is important for chemotaxis. If the bacterium tumbles too much, it spends too little time on actually moving away from the start point and won't be able to explore the space. If it tumbles too little, it might go too far in a wrong direction. 

The movement patterns of bacteria are dependent on the cell size, the gradient it experiences, and the fluid dynamics of the environment. The run-and-tumble movement is often observed in enteric and soil bacteria. For example, *Salmonella* bacteria (enteric) tumbles about once per second[^Achouri2015], *Enterococcus sacchrolyticus* (enteric) tumbles about per 1.2 seconds, *Bacillus subtilis* （soil and enteric) tumbles about every 2 seconds[^Turner2016], and *Rhizobia* (soil) tumbles per 1-2 seconds[^Gotz1987]. There is not a definite model for the differences on tumbling frequency between different species or among individuals in the same species yet. It is an interplay of some factors including but not limit to: cell size, speed, and obstacles in the environment[^Rashid2019][^Mitchell2005]. For example, more frequent tumbling for a large and fast cell; less frequent tumbling when more obstacles (reason not understood yet). Additionally, variation among individuals in the same species allows the cells to adapt to different gradient steepness better collectively[^Lim2019].

Despite the differences, the variations in tumbling frequency isn't large. There must be some reason why tumbling frequencies tend to average at about 1 tumble per second. We will return to this question at the close of the chapter. In the meantime, we will explore the biological basis of chemotaxis and try to explain why it has evolved the way it has. We will see that despite bacteria not being intelligent beings, the reality of how they achieve chemotaxis is far more complicated and sophisticated than we would imagine.


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

[^Gotz1987]: Gotz R and Schmitt R. 1987. *Rhizobium meliloti* swims by unidirectional, intermittent rotation of right-handed flagellar helices. J Bacteriol 169: 3146–3150. [Avaialbe online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC212363/)

[^Lim2019]: Lim S, Guo XK, Boedicker JQ. 2019. Connecting single-cell properties to collective behavior in multiple wild isolates of the *Enterobacter cloacae* complex. PLoS ONE 14(4): e0214719. [Avaialbe online](https://doi.org/10.1371/journal.pone.0214719)

[^Rashid2019]: Rashid S, Long Z, Singh S, Kohram M, Vashistha H, Navlakha S, Salman H, Oltvai ZH, Bar-Joseph Z. 2019. Adjustment in tumbling rates improves bacterial chemotaxis on obstacle-laden terrains. PNAS 116(24):11770-11775. [Available online](https://www.pnas.org/content/116/24/11770)

[^Mitchell2005]: Mitchell JG, Kogure K. 2005. Bacterial motility: links to the environment and a driving force for microbial physics. FEMS Microbiol Ecol 55(2006):3–16. [Available online](https://academic.oup.com/femsec/article/55/1/3/554107)

[Next Lesson: Biochemistry](home_biochem){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

