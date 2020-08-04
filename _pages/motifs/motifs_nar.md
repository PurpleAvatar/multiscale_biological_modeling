---
permalink: /motifs/nar
title: "The Negative Autoregulation Motif"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Hunting for a biological motivation for negative autoregulation

Theodosius Dobzhansky once wrote that "Nothing in biology makes sense except in the light of evolution." In the spirit of his quotation, there must be some evolutionary reason for the presence of so many negatively autoregulating transcription factors. Our goal is to use biological modeling to find this justification.

(CITE with link online:  Dobzhansky, Theodosius (March 1973), "Nothing in Biology Makes Sense Except in the Light of Evolution", American Biology Teacher, 35 (3): 125–129, JSTOR 4444260)

Say that we have two transcription factors *X* and *Y* with *X* regulating the transcription of *Y*, and consider two cells. In one cell, *X* regulates the transcription of *Y*; in the other, we have the additional fact that *Y* negatively autoregulates.

In this lesson, we are going to build a model simulating these two cellular environments, in which we examine the concentration of *Y*. In particular, we will simulate a "race" to the steady state concentration of *Y*. The cell that is able to reach this steady state faster is able to respond more quickly to its environment and therefore presumably more fit for survival.

## Modeling transcriptional regulation with chemical reactions

Recall from the [prologue](prologue) that we considered a program called MCell that could run randomized particle-based simulations via a reaction-diffusion model. We then visualized the results with CellBlender rendering software. We will use the same two software tools in this chapter to run our simulations.

In particular, to simulate *X* regulating the expression of *Y*, we will begin with a constant concentration of *X*. We then add a "reaction" *X* → *X* + *Y* at rate *p*<sub>*X*</sub> in order to simulate the up-regulation of *Y* by *X*. This reaction ensures that in a given interval of time there is some probability that a given *X* particle will spontaneously form a new *Y* particle; once again, we allow randomness to do its work for us.

We also will allow both *X* and *Y* particles to diffuse through the system at the same rate, although diffusion is not necessary for this simulation since the only reaction only involves single *X* reactants.

Finally, we should also take into account the fact that proteins are degraded by over time (by enzymes called **proteases**). Protein degradation offers a natural mechanism by which proteins at high concentrations can return to a steady-state. To this end, we will have a chemical reaction *Y* → *NULL* that removes *Y* particles in each unit of time according to some underlying probability. Because *X* is at steady-state, we assume that *X* is being produced at a rate that exactly balances its degradation rate, and we will therefore not need to add reactions to the model simulating the production or degradation of *X*.

**STOP:** What chemical reaction could be used to simulate negative autoregulation?

Negative autoregulation of *Y* means that the transcription factor corresponding to *Y* is able to bond to the upstream regions of the gene encoding *Y*, therefore slowing its transcription and lowering the concentration of *Y*. We can model this process with the hypothetical reaction 2*Y* → *Y*. In other words, when two *Y* particles encounter each other, there is some probability that one of the particles serves to remove the other, which mimics the process of a transcription factor turning another copy of itself off during negative autoregulation.

**STOP:** How many parameters do the two simulations have?

To recap, both of our simulations will include diffusion of *X* and *Y*, removal of *Y*, and the reaction *X* → *X* + *Y*. The simulation including negative autoregulation of *Y* will also include the reaction 2*Y* → *Y*. If you would like, you can run these simulations in the following tutorial. We will continue our discussion in the next section.

[Visit tutorial](tutorial_nar){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Ensuring the same steady-state concentration

If you followed the tutorial linked above, you were likely confused and disappointed in our negative autoregulating transcription factor *Y*. It may not be surprising that by allowing *Y* to turn itself off, we wound up with a simulation in which the final concentration of *Y* than in the case of only simple regulation of *Y* by *X*. It seems like we are back at square one; why in the world, then, would negative autoregulation be so common?

* NOAH: reproduce figure here showing the plot of *Y* under the two different simulations.

* (Should we cite mathematically controlled simulation?)


## Reflecting on negative autoregulation

The answer to the quandary posed in the previous section is that the model we have built was not controlled to ensure that a fair comparison between the two systems. In particular, it is critical that the two simulations that we build should be controlled so that they have approximately the *same* steady-state concentration of *Y*. Ensuring this equal footing for the two simulations is called a **mathematically controlled comparison.**

CITE SAVAGEAU 1976 https://ucdavis.pure.elsevier.com/en/publications/biochemical-systems-analysis-a-study-of-function-and-design-in-mo

**STOP:** How can we change the parameters of our models to obtain a mathematically controlled comparison?

There are a number of parameters that we should keep constant across the two models. First, the diffusion rates of *X* and *Y*, which we should keep constant across the two simulations. Second, the number of initial particles *X* and *Y*. And third, the degradation rate of *Y*.

The only way that we will be able to increase the steady-state concentration in the simulation involving autoregulation is if we increase the rate at which the reaction *X* → *X* + *Y* takes place. Finding the exact increase in this rate of reaction is an imperfect art form but can be obtained through trial and error.

* NOAH: review -- I don't know how we justify changing the steady-state any differently without getting into differential equations. How much do we need to change the parameters by to justify it?

* NOAH: We need an additional NAR tutorial linked from here in which we change the parameters by not enough, by too much, and finally getting a Goldilocks value. We should also be plotting the percentage of Y for the two simulations on the same plot.

## Results

* Phillip will return here to discuss the results. Alon's brake analogy would be good. Is there a better analogy that we can use?

* NOAH: Need to reproduce the image with the two different simulations overlaid on the same plot from the tutorial.

[Next lesson](feed){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Other
* Should be positive autoregulation somewhere at end of chapter.

* NOAH: How many positive autoregulation loops are there in our network?

* We also need a note at end of chapter about the fact that the cell is growing so that in more robust models the concentration is constantly decreasing as a result of the cell growing since it needs to double its volume every cell cycle.

* (Cite Alon book at some point -- when motifs are introduced? The introduction?)
