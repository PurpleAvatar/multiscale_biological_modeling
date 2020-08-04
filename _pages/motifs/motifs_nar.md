---
permalink: /motifs/nar
title: "The Negative Autoregulation Motif"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## A biological motivation for negative autoregulation

Theodosius Dobzhansky once wrote that "Nothing in biology makes sense except in the light of evolution." In the spirit of his quotation, there must be some evolutionary reason for the presence of so many negatively autoregulating transcription factors. Our goal is to use biological modeling to find this justification.

(CITE with link online:  Dobzhansky, Theodosius (March 1973), "Nothing in Biology Makes Sense Except in the Light of Evolution", American Biology Teacher, 35 (3): 125–129, JSTOR 4444260)

say that we have two transcription factors *X* and *Y* with *X* regulating the transcription of *Y*, and consider two cells. In one cell, *X* regulates the transcription of *Y*; in the other, we also have that *Y* negatively autoregulates.

We are going to build a model simulating these two cellular environments, isolated to the concentration of *Y*. In particular, we will simulate a "race" to the steady state concentration of *Y*. The cell that is able to reach this steady state faster is able to respond more quickly to its environment and therefore presumably more fit for survival.

* It is critical that as part of this simulation, we strive for the two systems to have the *same* steady-state concentration of *Y*. This way we keep as much as possible the same between the two simulations.

* Reminder of the prologue, where we considered a program that could run randomized simulations of particles via a reaction-diffusion model. (Pointer to tutorial on getting MCell and CellBlender installed.)

* We will use the same CellBlender program here that we used in the introduction in order to run our two simulations.  It may not seem what a reaction-diffusion simulation has to do with what we are doing here! But the ideas are the same.

* In particular, to simulate the regulation of *Y* by *X*, we will begin with a constant concentration of *X* and then add the chemical reaction *X* → *X* + *Y*.  This ensures that the concentration of *X* will stay constant, while in a given interval of time there is a probability *p*<sub>*X*</sub> that a given *X* particle will spontaneously generate a new *Y* particle.

* In the second simulation, in which we need to also consider negative autoregulation of *Y*, we should add a reaction that mimics this autoregulation.  The way in which we will do so is to add the reaction *2Y* → *Y*. In other words, when two *Y* particles collide, one of the particles serves to remove the other, which mimics the process of a transcription factor turning another copy of itself off as part of negative autoregulation. (Note: we will keep the reaction *X* → *Y* so that we do not see a decrease in the concentration of *Y*.

* Pointer to the tutorial on NAR [here](tutorial_nar)

## Results

* (Should we cite mathematically controlled simulation?)

* (Cite Alon book at what point?)



* Pointer to building something

* Brake analogy?

*Once CellBlender is installed and set-up, we can take a look at how ...something about NAR, motivations for NAR.*

### A Cell's Response

[Previous lesson](finding){: .btn .btn--primary .btn--large} [Next lesson](feed){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
