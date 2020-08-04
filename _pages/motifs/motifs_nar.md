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

In particular, to simulate *X* regulating the expression of *Y*, we will begin with a constant concentration of *X* that does not have a removal (
"kill") rate, ensuring that the concentration of *X* will remain constant throughout the simulation. We then add a "reaction" *X* → *X* + *Y* at rate *p*<sub>*X*</sub> in order to simulate the up-regulation of *Y* by *X*. This reaction ensures that in a given interval of time there is some probability *p*<sub>*X*</sub> that a given *X* particle will spontaneously form a new *Y* particle; once again, we allow randomness to do its work for us.

We also will allow both *X* and *Y* particles to diffuse through the system at the same rate, although diffusion is not necessary for this simulation since the only reaction only involves single *X* reactants.

* SOMETHING ABOUT THE REMOVAL RATE OF *Y*. Specify why this is biologically appropriate to have a removal rate.  Need to be careful and specify that we don't have a removal rate of *X* because we will assume that *X* is at steady-state already so that the kill and feed rates balance, and there's no sense in adding them.

**STOP:** What chemical reaction could be used to simulate negative autoregulation?

Negative autoregulation of *Y* means that the transcription factor corresponding to *Y* is able to bond to the upstream regions of the gene encoding *Y*, therefore slowing its transcription and lowering the concentration of *Y*. We can model this process with the hypothetical reaction 2*Y* → *Y*. In other words, when two *Y* particles encounter each other, there is some probability that one of the particles serves to remove the other, which mimics the process of a transcription factor turning another copy of itself off during negative autoregulation.

To recap, both of our simulations will include diffusion of *X* and *Y*, removal of *Y*, and the reaction *X* → *X* + *Y*. The simulation including negative autoregulation of *Y* will also include the reaction 2*Y* → *Y*. If you would like, you can run these simulations in the following tutorial. We will continue our discussion in the next section.

[Visit tutorial](tutorial_nar){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


## Ensuring the same steady-state concentration

If you followed the tutorial, you were likely confused and disappointed in our negative autoregulating transcription factor *Y*. It may not be surprising that by allowing *Y* to turn itself off, we wound up with a simulation in which the final concentration of *Y* than in the case of only simple regulation of *Y* by *X*. It seems like we are back at square one; why in the world would negative autoregulation be so common?

* NOAH: reproduce figure here showing the plot of *Y* under the two different simulations.

The answer is that our simulation did not have the appropriate

* (Should we cite mathematically controlled simulation?)


## Reflecting on negative autoregulation


* It is critical that as part of this simulation, we strive for the two systems to have the *same* steady-state concentration of *Y*. This way we keep as much as possible the same between the two simulations.



* Pointer to the tutorial on NAR [here](tutorial_nar)

## Results

* Brake analogy?

* (Cite Alon book at some point -- when motifs are introduced? The introduction?)


[Previous lesson](finding){: .btn .btn--primary .btn--large} [Next lesson](feed){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
