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

* The figure below illustrates that even with significant attempts to disrupt the number of particles in a system, the system returns to its oscillations within just a few cycles.

![image-center](../assets/images/nf_sim_interrupted.PNG){: .align-center}

* Robustness is a vital component of testing models of biological systems that need to be resilient to noise in order to ensure the stability of an organism's life processes.

* There is a bigger picture moral at hand, which is that if a biological system is robust, then we should be wary of trusting a fragile model of that system.

* In the next chapter, we will transition to a model of a bacterial cell's response to its environment that will involve more than three particles and require us to take into account many different reactions than we have in this section. A critical aspect of this model will be that it is robust.

[Next lesson](conclusion){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
