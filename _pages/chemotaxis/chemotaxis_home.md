---
permalink: /chemotaxis/home
title: "Introduction to Chemotaxis"
sidebar:
 nav: "chemotaxis"
---

### by Shuanger Li and Phillip Compeau

## Lost Immortals

The book *What If?*[^Munroe] compiles a collection of crazy hypotheticals, along with enthusiastically scientific replies from the author. Below is one such quandary:

> If two immortal people were placed on opposite sides of an uninhabited Earth-like planet, how long would it take them to find each other? 100,000 years? 1,000,000 years?

**STOP:** What would you propose that the two immortals could do to find each other?
{: .notice--primary}

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

Like other prokaryotes, *E. coli* are small, with a length about 2µm, and a diameter 0.25-1µm.[^Pierucci1978] This puts them into the same situation like the Lost Immortals or the ants exploring the world: the environment in which they need to find food is huge; food is sparsely distributed; and they are small. The answer is the chemotaxis behavior.

The behavior of cells moving towards or away from a substance is called **chemotaxis**. For *E. coli*, moving towards attractants (ex. glucose, electron acceptors), and moving away from repellents (ex. Ni<sup>2+</sup>, Co<sup>2+</sup>) are all considered chemotaxis behaviors.

Here is a cute video of *E. coli* moving towards a sugar crystal.
<iframe width="640" height="360" src="https://www.youtube.com/embed/F6QMU3KD7zw" frameborder="0" allowfullscreen></iframe>

## How does *E. coli* explore the world?

*E. coli* has 5-12 flagelli randomly distributed in the surface.[^Sim2017] Each flagelum rotates clockwise (CW) or counter-clockwise (CCW). That leads to two states of movement: 1) when flagelli rotates in CCW, they form a bundle, and propel the cells to swiming smoothly at speeds of 20 µm per second, called **run**; 2) when some flaggeli in the bundle rotates CW, the flagelli become uncoordinated and reorients with a much slower net movement speed in place, called **tumble**.[^Baker2005]

![image-center](../assets/images/chemotaxis_intro_runtumble.png){: .align-center}
<figcaption>Run and tumble. Image from Parkinson Lab, University of Utah.</figcaption>

In a uniform environment, *E. coli* tumbles once about every 1-1.5 seconds.[^Weis1990][^Berg2000] Such tumbling frequency is clever, because if the bacteria tumble too much, it won't be able to explore the space; but if it tumbles too little, it might go too far in the wrong direction. Other flagellated motile bacteria uses similar exploration mechanisms; for example, *Salmonella* bacteria tumbles about once per second[^Achouri2015], *Bacillus subtilis* tumbles about every 2 seconds, *Enterococcus sacchrolyticus* tumbles about per 1.2 seconds.[^Turner2016]

[Next Lesson: Biochemistry](home_intro){: .btn .btn--primary .btn--large}
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

