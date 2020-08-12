---
permalink: /motifs/nar
title: "The Negative Autoregulation Motif"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Hunting for a biological motivation for negative autoregulation

Theodosius Dobzhansky once wrote that "Nothing in biology makes sense except in the light of evolution."[^Dob] In the spirit of his quotation, there must be some evolutionary reason for the presence of so many negatively autoregulating transcription factors. Our goal is to use biological modeling to find this justification.

Say that we have two transcription factors *X* and *Y* with *X* regulating the transcription of *Y*, and consider two cells. In one cell, *X* regulates the transcription of *Y*; in the other, we have the additional fact that *Y* negatively autoregulates.

In this lesson, we are going to build a model simulating these two cellular environments, in which we examine the concentration of *Y*. In particular, we will simulate a "race" to the steady state concentration of *Y*. The cell that is able to reach this steady state faster is able to respond more quickly to its environment and therefore presumably more fit for survival.

## Modeling transcriptional regulation with chemical reactions

Recall from the [prologue](prologue) that we considered a program called MCell that could run randomized particle-based simulations via a reaction-diffusion model. We then visualized the results with CellBlender rendering software. We will use the same two software tools in this chapter to run our simulations.

In particular, to simulate *X* regulating the expression of *Y*, we will begin with a constant concentration of *X*. We then add a "reaction" *X* → *X* + *Y* at rate *p*<sub>*X*</sub> in order to simulate the up-regulation of *Y* by *X*. This reaction ensures that in a given interval of time there is some probability that a given *X* particle will spontaneously form a new *Y* particle; once again, we allow randomness to do its work for us.

We also will allow both *X* and *Y* particles to diffuse through the system at the same rate, although diffusion is not necessary for this simulation since the only reaction only involves single *X* reactants.

Finally, we should also take into account the fact that proteins are degraded by over time (by enzymes called **proteases**). Protein degradation offers a natural mechanism by which proteins at high concentrations can return to a steady-state. To this end, we will have a chemical reaction *Y* → *NULL* that removes *Y* particles in each unit of time according to some underlying probability. Because *X* is at steady-state, we assume that *X* is being produced at a rate that exactly balances its degradation rate, and we will therefore not need to add reactions to the model simulating the production or degradation of *X*.

**STOP:** What chemical reaction could be used to simulate negative autoregulation?
{: .notice--primary}

Negative autoregulation of *Y* means that the transcription factor corresponding to *Y* is able to bond to the upstream regions of the gene encoding *Y*, therefore slowing its transcription and lowering the concentration of *Y*. We can model this process with the hypothetical reaction 2*Y* → *Y*. In other words, when two *Y* particles encounter each other, there is some probability that one of the particles serves to remove the other, which mimics the process of a transcription factor turning another copy of itself off during negative autoregulation.

**STOP:** How many parameters do the two simulations have?
{: .notice--primary}

To recap, both of our simulations will include diffusion of *X* and *Y*, removal of *Y*, and the reaction *X* → *X* + *Y*. The simulation including negative autoregulation of *Y* will also include the reaction 2*Y* → *Y*. If you would like, you can run these simulations in the following tutorial. We will continue our discussion in the next section.

[Visit tutorial](tutorial_nar){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Ensuring the same steady-state concentration

If you followed the tutorial, you were likely confused and disappointed in our negative autoregulating transcription factor *Y*. It may not be surprising that by allowing *Y* to turn itself off, we wound up with a simulation in which the final concentration of *Y* is less than in the case of only simple regulation of *Y* by *X*. It seems like we are back at square one; why in the world, then, would negative autoregulation be so common?

![image-center](../assets/images/nar_unequal_graph.PNG){: .align-center}

The answer to the quandary posed in the previous section is that the model we have built was not controlled to ensure that a fair comparison between the two systems. In particular, it is critical that the two simulations that we build should be controlled so that they have approximately the *same* steady-state concentration of *Y*. Ensuring this equal footing for the two simulations is called a **mathematically controlled comparison.**[^Savageau]

**STOP:** How can we change the parameters of our models to obtain a mathematically controlled comparison?
{: .notice--primary}

There are a number of parameters that we must keep constant across the two models. First, the diffusion rates of *X* and *Y*, which we should keep constant across the two simulations. Second, the number of initial particles *X* and *Y*. And third, the degradation rate of *Y*.

The only way that we will be able to increase the steady-state concentration in the simulation involving autoregulation is if we increase the rate at which the reaction *X* → *X* + *Y* takes place. Finding the exact increase in this rate of reaction is an imperfect art form but can be obtained through trial and error.

[Visit tutorial](tutorial_nar#Matching-Steady-States){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

* NOAH: review -- I don't know how we justify changing the steady-state any differently without getting into differential equations. How much do we need to change the parameters by to justify it?

If you followed the tutorial on using CellBlender to visualize the two simulations, then you may want to try your hand at adjusting this parameter and seeing what happens. If you would like to follow along with our tutorial building a mathematically controlled comparison, then follow the link below.

* NOAH: We need an additional NAR tutorial here in which we change the parameters by not enough, by too much, and finally getting a Goldilocks value. We should also be plotting the percentage of Y for the two simulations on the same plot.

## Results

The figure below shows a plot of the amount of *Y* for the two simulations on the same chart over time. Now that we are able to obtain the same steady-state concentration of *Y* in the two simulations, a justification for negative autoregulation appears.

![image-center](../assets/images/nar_equal_graph.PNG){: .align-center}

The simulation with negative autoregulation starts with a low concentration of *Y*. For this reason, because the rate of the reaction *X* → *X* + *Y* is higher in the negative autoregulation simulation, the number of *Y* particles in this simulation increases much faster.

As the concentration of *Y* increases, the rate at which new *Y* are being added to the system remains constant because it depends only upon *Y*. However, the rate at which *Y* are being removed increases because we have not only the degradation reaction *Y* → *NULL* but also the negative autoregulation reaction 2*Y* → *Y*, both of which depend on the current number of *Y* particles present in the system. As a result, the curve flattens more quickly for the simulation involving negative autoregulation.

More importantly, we now understand *why* negative autoregulation has evolved. Because the simulation involving negative autoregulation wins the "race" to steady-state concentration of *Y*, we can conclude that a cell in which a transcription factor is negatively autoregulated has higher evolutionary fitness than one that does not.

An excellent analogy proposed by Uri Alon for negative autoregulation is that of a car with a powerful engine (the higher rate of the reaction *X* → *X* + *Y*) and sensitive brakes (the reaction 2*Y* → *Y* that causes *Y* to quickly reach a steady-state concentration). This is reinforced by the plot below, where we show that we can reach steady-state even more quickly if we increase the rate of both of these reactions while keeping the steady-state concentration constant.

* NOAH: show plots for a couple of additional NAR simulations, where we keep increasing the two reaction rates. (May need multiple colors.)

In this section, we have seen that particle-based simulations can be powerful for justifying why a network motif is prevalent. In the remainder of this chapter, we will simulate two more commonly occurring network motifs and analyze these simulations to determine why these motifs have evolved.

[Next lesson](feed){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Other
* In Noah's second tutorial, Phillip will have a question at the end of the tutorial asking the user to draw the conclusion on their own.

* In the results section, should say something about their being practical limitations to how much we can increase the reaction producing *Y*, which provides a trade-off hence why the reaction rate isn't higher.

* Should be positive autoregulation somewhere -- how many positive autoregulation loops are there?

* NOAH: Just curious... how many positive autoregulation loops are there in our network?

* (Cite Alon book at some point -- when motifs are introduced? The introduction?)

[^Dob]: Dobzhansky, Theodosius (March 1973), "Nothing in Biology Makes Sense Except in the Light of Evolution", American Biology Teacher, 35 (3): 125–129, JSTOR 4444260)

[^Savageau]: Savageau, 1976 https://ucdavis.pure.elsevier.com/en/publications/biochemical-systems-analysis-a-study-of-function-and-design-in-mo
