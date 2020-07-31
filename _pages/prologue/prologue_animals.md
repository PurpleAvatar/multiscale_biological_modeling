---
permalink: /prologue/animals
title: "Back to Zebras"
sidebar:
 nav: "prologue"
toc: true
toc_sticky: true
---

## Turing patterns

In the previous section, we introduced a random walk, which serves as a model of a particle diffusing through a medium as a result of Brownian motion. What exactly does this have to do with zebras?

Turing's insight was that remarkable patterns would emerge if we combine diffusion with a simulated chemical reaction, in which particles interact with each other as they diffuse. Such a model is called a **reaction-diffusion system**, and the patterns that emerge in the simulation are called **Turing patterns** in Turing's honor.

## An example reaction-diffusion system

Let us consider an example of a reaction-diffusion system. We will have two types of particles, *A* and *B*; you may like to think of *A* as a predator and *B* as a prey. The system is not representing a predator-prey relationship, and the reason why we think of these molecules as predator and prey will become clear soon.

Both types of particles diffuse randomly through the plane, but the *B* particles diffuse twice as quickly as the *A* particles.  In terms of a random walk, this means that in a single diffusion "step", an *A* particle moves twice as far.

**STOP**: Say that we release one *A* particle and one *B* particle at the same location. On average, how much farther from the origin will *A* be than *B*?

We now will add some reactions to our system. The *B* particles are "fed" into the system at some constant rate *f*. This means that in a unit of time, the concentration of *B* particles in the system will increase by *f*.

Similarly, there is another constant rate *k* dictating a "death" rate of the *B* particles; in a unit of time, the concentration of *B* particles in the system will decrease by *k* due to a subset of the *B* particles being chosen for removal from the system.

(Question for Noah: Is there a better explanation of these?)

Finally, the system has a single reaction of the two particles with each other. If an *A* particle and two *B* particles encounter each other, then the *A* particle is replaced by a third *B* particle. This reaction can be summarized by the following chemical reaction.

$$A + 2B \rightarrow 3B$$

This reaction is why we compared *A* to prey and *B* to predators, since we can imagine this reaction as two *B* particles consuming an *A* particle and conceiving an offspring *B* particle.

(Question for Noah: Is the rate of this reaction important?  What are its units in CellBlender?)

## Changing parameters influence the macro behavior of the reaction-diffusion system

Our plan is to initiate the system with a uniform concentration of *A* particles spread across the grid, then add a mass of *B* particles to the center of the grid.  But before we do this, we point out that the end result of this animation will vary depending upon a few things.

A **parameter** is a variable quantity used as input to a model. Parameters are inevitable in biological modeling (and data science in general), and as we will see, changing parameters can cause major changes in the behavior of a system.

Note that there are three parameters relevant to our reaction-diffusion system. Two of these parameters are the feed rate (*f*) of *A* particles and the kill rate of the *B* particles (*k*). The third parameter of interest corresponds to the diffusion rates of the two types of particle. We report this as a single parameter because the diffusion rates are completely dependent on each other; once the diffusion rate of the *B* particles is set, the diffusion rate of *A* particles will be twice that of the *B* particles.

You can think of all these parameters as dials we can turn, observing how the system changes on a macro level. For example, if we raise the diffusion rate, then the particles will be moving around more, which means that we will see more of the reaction *A* + 2*B* → 3*B*.

**STOP:** What will happen as we increase or decrease the feed rate *f*? What about the kill rate *k*?

For some parameter values, our system is not particularly interesting.  For example, the following animation shows that if *k* is too high, then the *B* particles will die out more quickly than they are replenished by the reaction with *A* particles, and so only *A* particles will be left. In this animation, *A* particles have been colored green and *B* particles have been colored red.

(INSERT VIDEO SHOWING PREY THRIVING AND PREDATORS DYING OUT. Indicate parameters.)

On the other hand, if *f* is too high, then there will be an increase in the *A* particles. However, there will also be more interactions between *A* particles and pairs of *B* particles, and so we will then see an explosion in the number of predators.

(INSERT VIDEO, with parameters indicated)

The interesting behavior in this system lies in a sweet spot, where we see interesting macro behavior of the system when

* The interesting behavior lies in a “sweet spot”: values of the four parameters that produce interesting macro behavior when we examine the system at a macro level.

(INSERT 3-4 MERT VIDEOS, WITH CLEAR EXPLANATION OF PARAMETERS EACH TIME)

* This behavior is remarkable first and foremost because we can pick out so much organization from tens of thousands of tiny particles. But it also is amazing that the system is so fine-tuned, meaning that very slight changes in parameter values can lead to significant changes in the overall system, which in this case is a change between spots and stripes.
* In fact, later in the course, we will see an example of a biological system that is not fine-tuned, but rather robust: variation in the system does not lead to substantive changes in the ultimate behavior of the system.
* The emergence of patterns from such a simple model was Turing’s essential contribution in the 1950s, and one that has been borne out both by biological research, which has found a molecular basis for the two-particle model in the development of some organisms, as well as evidence that the system is fine-tuned.
* For example, note the following photos of two giant pufferfish.

(Phillip will insert picture.)

* These two fish are genetically very similar, but one has stripes and the other spots. What seems like an enormous change in the appearance of an organism can actually be attributable to a small change of parameters in a fine-tuned system that is powered solely by randomness.

(Phillip will insert Turing quote on the horse part being the hard part)

WE WILL MAKE LEARNER WAIT UNTIL THEY CAN IMPLEMENT THIS AT A LATER TIME

[Previous](random-walk){: .btn .btn--primary .btn--x-large} [Next Page](blocks){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
