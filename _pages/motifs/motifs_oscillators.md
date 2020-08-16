---
permalink: /motifs/oscillators
title: "Building a Biological Oscillator"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Oscillators are everywhere in nature

* Humans, when placed in a bunker, maintain a roughly 24-hour cycle of sleep and activity (CITE)

* But **circadian rhythms** like these are visible throughout living things, even in cyanobacteria (CITE)

* Furthermore, cyclic life processes are not confined to circadian rhythms. Your heart and respiratory systems follow a cyclical process without you even thinking about it, and of course the cell cycle offers another example on a smaller scale across all cells.

* The underlying principle that unites all of these cyclical processes is **oscillation**. As one quantity rises, another falls, and the process cycles naturally by itself without any additional external process influencing it.

* We know that there isn't an intelligence driving these cyclic processes, and in fact they must be built upon very simple components.

## The repressilator

* There are many examples of network motifs that facilitate oscillation, some of which are very complicated with many moving parts. We will focus on a simple three-component oscillator motif called a **repressilator** (CITE).

* We will see how to implement this oscillator using a particle simulator but we will also analyze its *robustness* in contrast to the *fine-tuned* system for developing Turing patterns considered in the [prologue](prologue).

* The structure of a repressilator is shown in the figure below. In this motif, all three proteins are transcription factors, and they form a cycle in which *X* represses *Y*, *Y* represses *Z*, and *Z* represses *X* (hence the name).

* INSERT FIGURE.

* The repressilator certainly includes feedback, but nothing about this motif would indicate *a priori* that it would lead to oscillation.

**STOP:** Try building a reaction-diffusion model for the repressilator, assuming that we start with an initial concentration of *X* and no *Y* or *Z* particles.
{: .notice--primary}

## Modeling a repressilator with a reaction-diffusion particle simulation

* Building a model for the repressilator.

* We begin with a quantity of *X* particles, and no *Y* or *Z* particles.

* NOAH: is this right that we start with no *Y* or *Z*, or is it just a low concentration?

* *X*, *Y*, and *Z* all diffuse at the same rate.

* These particles are all produced as the result of activation by some other transcription factor(s), which we will assume happens at same rate. We will model this by having hidden particles *I* that all serve to active our three particles by the reactions *I* → *I* + *X*, *I* → *I* + *Y*, and *I* → *I* + *Z*, all taking place at the same rate.

* Furthermore, *X*, *Y*, and *Z* all have a degradation rate, which is the same for all three particles.

* This leaves us the repression reactions, which are represented by *X* + *Y* → *X*, *Y* + *Z* → *Y*, and *Z* + *X* → *Z*.

* You probably know enough to model the reaction-diffusion reaction modeling the repressilator yourself, but we will provide a tutorial if you find it helpful.

* NOAH: please link to repressilator tutorial 1 here.

## The oscillations of the repressilator

* In the figure below, we show the results of running our simulation by plotting the number of *X*, *Y*, and *Z* particles.

* NOAH: provide figure with the oscillations.

* As we can see, the system oscillates, with a high concentration of *X*, *Y*, and *Z* taking turns before repeating.

**STOP:** Why do you think that the repressilator leads to the pattern of oscillations in the figure above?
{: .notice--primary}

* A natural question is why the structure of the repressilator would cause the three particles to take turns at high concentrations, so let us consider each particle one at a time.

* Because *X* starts out high, as soon as there are some *Z* particles the repressing reaction *Z* + *X* → *Z* starts to decrease the amount of *X*.

* Furthermore, because there are a lot of *X* particles, the reaction *X* + *Y* → *X* prevents the number of *Y* particles from growing.

* However, there are very few *Y* or *Z* particles at the start, and so the third repression reaction *Y* + *Z* → *Y* has very little effect on the concentration of *Z*, and so the number of *Z* particles grows.

* The end result is that the concentration of *X* plummets, with the concentration of *Z* rising up to replace it, accounting for the second peak in the figure.

* As a result, *Z* and *X* in effect switch roles.  Now the reaction *Y* + *Z* → *Y* will decrease the amount of *Z*, and because there are not many *X* or *Y* particles, the reaction *X* + *Y* → *X* does not occur often, meaning that the concentration of *Y* will rise, accounting for the third peak in the figure.

* Finally, because *Y* is at high concentration, the reaction *X* + *Y* → *X* will occur much more often than the reaction *Z* + *X* → *Z*. Therefore, the concentration of *Y* will decrease while the concentration of *X* increases.  This accounts for the fourth peak in the figure and returns the simulation to its original situation, at which point the cycle will start again.

## Engineering a repressilator

* NOAH: we need to have an overview of the repressilator experiment from 2000, which apparently was refined in 2000.  Could you give a short overview of how it works here?

* It is amazing that such a simple motif can produce oscillations and be integrated synthetically into a living cell, but there is an even more fascinating aspect of biological oscillators that we will discuss in the next section.

[Next lesson](robust){: .btn .btn--primary .btn-large}
{: style="font-size: 100%; text-align: center;"}
