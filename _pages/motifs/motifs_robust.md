---
permalink: /motifs/robust
title: "Modeling Oscillator Robustness"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## The need for robustness in biological oscillators

Nothing exemplifies the need for robustness in biological systems better than oscillators. If a palpitation causes your heart to skip a beat, it should be able to return quickly to its natural rhythm. If you hold your breath to dive underwater on a snorkeling tip, you shouldn't hyperventilate when you return to the surface. And regardless of what functions your cells perform or what disturbances they find in their environment, they should be able to maintain a normal cell cycle.

An excellent illustration of the robustness of the circadian clock is the body's ability to handle jet lag. There is no apparent reason why you would have evolved to fly halfway around the world and be able to return to a normal daily cycle after just a few days of fatigue.

In the previous lesson, we saw that the repressilator will produce oscillations even in a noisy environment. This leads us to wonder about the extent to which our repressilator is robust, and how quickly it can respond to a disturbance.

## A coarse-grained model for reaction-diffusion

We have noted that a benefit of using a reaction-diffusion particle model to study network motifs is the inclusion of built-in noise to ensure a measure of robustness. However, a downside of such a model is that simulating the movements of so many particles leads to a slow simulation that does not scale well to many particles or reactions.

Although our model is ultimately interested in the interactions of molecules, the conclusions we have made throughout this chapter are only based on the *concentrations* of these particles. Therefore, as we did in the [prologue](prologue), we might imagine developing a coarser-grained version of our model that allows us to make faster conclusions about particle concentrations without keeping track of the diffusion of individual particles.

For example, say that we are modeling a degradation reaction. If we start with 10,000 *X* particles, then after a single time step, we can simply multiply the number of *X* particles by (1-*r*) where *r* is a parameter related to the rate of the degradation reaction.

As for a repression reaction like *X* + *Y* → *X*, say that the concentrations of *X* and *Y* are uniform throughout the object and the diffusion rates of *X* and *Y* are the same. We can update the concentration of *Y* particles by subtracting some factor times the current concentration of *Y* particles. This factor should be directly related to the current concentrations of both *X* and *Y*.

The technical details behind such a coarse-grained model are beyond the scope of our work in this lesson, but we will return to these technical details in the next module. In the meantime, we provide a tutorial below showing how to build a particle-free simulation replicating the repressilator motif. As part of this tutorial, we will make a major disturbance to the concentration of one of the particles and see how long the disturbance lasts and whether the particle concentrations can resume their oscillations.

[Visit tutorial](tutorial_perturb){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## The repressilator is robust to disturbance

In the figure below, we show a plot of concentrations of each particle in our coarse-gained simulation of the repressilator, with one caveat.  Midway through the simulation, we incorporate a disturbance that causes a spike in the concentration of *Y*.

![image-center](../assets/images/nf_sim_interrupted.PNG){: .align-center}
<figcaption>Adding a significant number of *Y* particles to our simulation produces little ultimate disturbance to the concentrations of the three particles, which return to normal oscillations within a single cycle.</figcaption>

Because of the spike in the concentration of *Y*, the reaction *Y* + *Z* → *Y* suppresses the concentration of *Z* for longer than usual, and so the concentration of *X* is free to increase for longer than normal. As a result, the next peak in the concentration of *X* is higher than normal.

We might hypothesize that this process would continue, with a tall peak in the concentration of *Z*. However, the peak in the concentration of *Z* is no taller than normal, and the next peak shows a normal concentration of *X*. In other words, the system has very quickly absorbed the blow of an increase in concentration of *Y* and returned to normal within one cycle.

* NOAH: do we have a good high-level explanation for what causes the oscillations to return to normal?

In fact, even with a much larger jolt to the repressilator, we observe the concentrations of the three particles return to normal oscillations very quickly.

* NOAH: can you show one more figure that shows an even bigger shock to the system?

The repressilator is not the only network motif that leads to oscillations in particle concentrations, but robustness to disturbances in these concentrations is a shared feature of all these motifs.

* NOAH: Cite? Example?

The robustness of our repressilator model also implies a bigger picture moral in biological modeling. If an underlying biological system demonstrates robustness to change, then any model of that system should also be able to withstand this change. Conversely, we should be wary of any model of a robust system that is overly sensitive to changes in the system.

In this module, we have seen that even very simple network motifs can have a powerful effect on a cell's ability to implement elegant systems of behavior. In the next module, we will encounter a much more involved biochemical process, with far more molecules and reactions, that is used by bacteria to cleverly (and robustly) explore their environment. In fact, we will have so many reactions that we will need to rethink how we set up our model. We hope that you will join us!

In the meantime, check out the exercises below to continue developing your understanding of how transcription factor network motifs have evolved.

[Next module](../chemotaxis/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

* In the next chapter, we will transition to a model of a bacterial cell's response to its environment that will involve more than three particles and require us to take into account many different reactions than we have in this section. A critical aspect of this model will be that it is robust.

[Next lesson](conclusion){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
