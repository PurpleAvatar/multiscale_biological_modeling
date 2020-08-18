---
permalink: /motifs/oscillators
title: "Building a Biological Oscillator"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Oscillators are everywhere in nature

Even if placed in a bunker, humans will maintain a roughly 24-hour cycle of sleep and wakefulness. However, such a **circadian rhythm** is not unique to humans or even animals but rather is present throughout living things, including plants and even cyanobacteria.

* NOAH: cite the bunker experiment: Aschoff, J. (1965). Circadian rhythms in man. Science 148, 1427–1432.

* NOAH: also cite the first paper that found circadian rhythm in cyanobacteria: Grobbelaar N, Huang TC, Lin HY, Chow TJ. 1986. Dinitrogen-fixing endogenous rhythm in Synechococcus RF-1. FEMS Microbiol Lett 37:173–177. doi:10.1111/j.1574-6968.1986.tb01788.x.CrossRefWeb of Science.

Life processes like the circadian rhythm that **oscillate** between different states are not confined to circadian rhythms. You may feel like you have some control over when you go to bed, but your heart and respiratory system both follow cyclical rhythms without you even thinking about it. On a much lower level, eukaryotic cells are governed by a strict cell cycle as the cells grows and divide.

We know that there is no intelligence that drives all these cyclic processes, and we might guess from what we have learned in this module that they must be built upon simple rules serving as a **pacemaker** controlling the oscillations. However, the question remains as to what these pacemakers are.

We also suspect that these rhythms also must be *robust*. That is, they should be resilient to small changes in order to be executed correctly many times over an organism's life. But how is this robustness achieved?

## The repressilator: a synthetic biological oscillator

Researchers have identified many network motifs that facilitate oscillation, some of which are very complicated and include many components. In this lesson, we will focus on a simple three-component oscillator motif called a **repressilator**. We will implement the repressilator with a particle simulator but also then analyze the robustness of this system in response to small changes in concentrations of particles.

* CITE repressilator.

The repressilator motif is shown in the figure below. In this motif, all three proteins are transcription factors, and they form a cycle in which *X* represses *Y*, *Y* represses *Z*, and *Z* represses *X* (hence the name). The repressilator clearly forms a feedback loop, but nothing *a priori* about this motif would indicate that it would lead to oscillation; after all, we have already seen feedback processes in this module that did not lead to oscillation.

<center>
<img src="../assets/images/repressilator.png" width="250">
<figcaption>The repressilator motif for three particles <em>X</em>, <em>Y</em>, and <em>Z</em>. <em>X</em> represses <em>Y</em>, which represses <em>Z</em>, which in turn represses <em>X</em>, forming a feedback loop.</figcaption>
</center>

**STOP:** Try building a reaction-diffusion model for the repressilator, assuming that we start with an initial concentration of *X* and no *Y* or *Z* particles.
{: .notice--primary}

## Modeling a repressilator with a reaction-diffusion particle simulation

To build a reaction-diffusion model accompanying the repressilator, we start with a quantity of *X* particles, and no *Y* or *Z* particles. We then assume that all three particles diffuse at the same rate and degrade at the same rate.

Furthermore, we assume that all three particles are produced as the result of an activation process by some other transcription factor(s), which we assume happens at the same rate. We will use a single type of particle *I* that will be hidden and serves to activate the three visible particles by the reactions *I* → *I* + *X*, *I* → *I* + *Y*, and *I* → *I* + *Z*.

In the previous lesson on the feed-forward loop, we saw that to model a repression of *Y* by *X*, we can use the reaction *X* + *Y* → *X*. We combine this reaction with the additional two reactions *Y* + *Z* → *Y*, and *Z* + *X* → *Z* to complete the repressilator model.

If you have followed our previous tutorials, then you may feel comfortable taking off the training wheels and trying out implementing the repressilator on your own. We also are more than happy to provide a tutorial if you find it useful.

[Visit tutorial](tutorial_oscillators){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## The oscillations of the repressilator

The figure below shows the results of our simulation by plotting the number of *X*, *Y*, and *Z* particles over time. As we can see, the system shows clear oscillatory behavior, with the concentrations of *X*, *Y*, and *Z* taking turns being at high concentration.

**STOP:** Why do you think that the repressilator motif leads to this pattern of oscillations?
{: .notice--primary}

![image-center](../assets/images/repress_graph.PNG){: .align-center}

* NOAH: please provide a caption with colors of particles indicated.

* NOAH: A natural question is what the period of this oscillation is and how this connects to real examples from the original repressilator paper.  Don't get in the weeds on this (max 10 minutes, but lmk what you think.)

* START HERE

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
