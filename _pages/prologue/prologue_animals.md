---
permalink: /prologue/animals
title: "A Reaction-Diffusion Model and Turing Patterns"
sidebar:
 nav: "prologue"
toc: true
toc_sticky: true
---

## From random walks to reaction-diffusion

In the previous section, we introduced a random walk, which serves as a model of a particle diffusing through a medium as a result of Brownian motion. But what exactly does diffusion of particles have to do with Alan Turing and zebras?

Turing's insight was that remarkable patterns would emerge if we combine a simulation of diffusion with a chemical reaction, in which particles interact with each other as they diffuse. Such a model is called a **reaction-diffusion system**, and the patterns that emerge in the simulation are called **Turing patterns** in Turing's honor.

## An example reaction-diffusion system

We will consider a reaction-diffusion system having two types of particles, *A* and *B*. The system is not representing a predator-prey relationship, but you may think of *A* as a predator and *B* as a prey for reasons that will become clear soon.

Both types of particles diffuse randomly through the plane, but the *B* particles diffuse twice as quickly as the *A* particles.  In terms of the random walk, this faster diffusion means that in a single "step", an *A* particle moves twice as far as a *B* particle.

**STOP**: Say that we release one *A* particle and one *B* particle at the same location. On average, how much farther from the origin will *A* be than *B* after *n* steps?
{: .notice--primary}

We now will add some reactions to our system. The *A* particles are added into the system at some constant **feed rate** *f* (these particles are created as the result of other reactions). In a three-dimensional system, the units of *f* would be in mol/L/s, which means that every second, there are *f* moles of particles added to the system in every liter of volume. (Recall that one mole is 6.02214076 · 10<sup>23</sup>.) This means that in a given unit of time, the number of *A* particles in the system will increase by a constant number.

There is also a **death rate** constant *k* dictating the rate of removal of the *B* particles. As a result of removal, the concentration of *B* particles in the system will decrease by approximately a constant factor in a given time step.

Note that there is a slight difference between the two reactions. In the first reaction, the *number* of *A* particles increases by a constant factor at every step. In the second reaction, the *concentration* of *B* particles decreases by a constant factor at every step. This means that if *A* and *B* denote the number of particles of each type in the system, then

<center>
<em>dA</em>/<em>dt</em> = <em>c</em><sub>1</sub> · <em>A</em>
</center>

and

<center>
<em>dB</em>/<em>dt</em> = <em>c</em><sub>1</sub> · <em>B</em> .
</center>

Finally, this reaction-diffusion system has a single reaction of the two particles with each other. If an *A* particle and two *B* particles encounter each other, then the *A* particle is replaced by a third *B* particle at a certain rate *r*. This reaction can be summarized by the following chemical reaction.

<center><em>A</em> + 2<em>B</em> → 3<em>B</em><br></center>

This reaction is why we compared *A* to prey and *B* to predators, since we can imagine this reaction as two *B* particles consuming an *A* particle and conceiving an offspring *B* particle. Another way of viewing this reaction is that when an *A* particle and two *B* particles encounter each other, the reaction takes place with probability proportional to *r*.

* NOAH: we need to better understand the correspondence between reaction rates and probabilities in MCell.

* NOAH: this is where the link to the reaction-diffusion tutorial should go I think.

## Changing parameters influence the macro behavior of the reaction-diffusion system

Our plan is to initiate the system with a uniform concentration of *A* particles spread across the grid, and then add a collection of *B* particles to the center of the grid.  But before we do this, we first point out that the results of this simulation may vary depending upon a few things.

A **parameter** is a variable quantity used as input to a model. Parameters are inevitable in biological modeling (and data science in general), and as we will see, changing parameters can cause major changes in the behavior of a system.

Note that there are four parameters relevant to our reaction-diffusion system. Three of these parameters are the feed rate (*f*) of *A* particles, the kill rate of the *B* particles (*k*), and the rate of the predator-prey reaction (*r*). The final parameter of interest corresponds to the diffusion rates of the two types of particle. We report this as a single parameter because the diffusion rates are completely dependent on each other; once the diffusion rate of the *B* particles is set, the diffusion rate of *A* particles will be twice that of the *B* particles.

You can think of all these parameters as dials we can turn, observing how the system changes on the macro level. For example, if we raise the diffusion rate, then the particles will be moving around and bouncing into each other more, which means that we will see more of the reaction *A* + 2*B* → 3*B*.

**STOP:** What will happen as we increase or decrease the feed rate *f*? What about the kill rate *k*?
{: .notice--primary}

For some parameter values, the system is not particularly interesting.  For example, the following animation is produced for *k* = 500,000 and *f* = 10. It shows that if *k* is too high, then the *B* particles will die out more quickly than they are replenished by the reaction with *A* particles, and so only *A* particles will be left. In this animation, *A* particles have been colored green, and *B* particles have been colored red.

* NOAH: what is the reaction rate *r* for the predator-prey reaction? What is the diffusion rate?  Units? Width of grid?

<iframe width="640" height="360" src="../assets/mert_predator_dies_f1e1_r5e5.mp4" frameborder="0" allowfullscreen></iframe>
*f* = 10 and *k* = 500,000
{: .text-center}

On the other hand, if *f* is too high, then there will be an increase in the *A* particles. However, there will also be more interactions between *A* particles and pairs of *B* particles, and so we will then see an explosion in the number of predators.

* NOAH: This video is fascinating!  I think you are in the sweet spot though -- the whole point was to jack up the value of *f* which appears not to have been done. What happens at say *f* = 100?

<iframe width="640" height="360" src="../assets/mert_prey_dies_f1e1_r1e5.mp4" frameborder="0" allowfullscreen></iframe>
*f* = 10 and *r* = 100,000
{: .text-center}

The interesting behavior in this system lies in a sweet spot, where we see interesting macro behavior for a given collection of parameters.

For example,

* NOAH: INSERT MERT VIDEO WITH CLEAR EXPLANATION OF PARAMETERS
<iframe width="640" height="360" src="../assets/gray_scott_test.mp4" frameborder="0" allowfullscreen></iframe>
Parameters unknown
{: .text-center}

And yet if we make a slight change to the parameters, we obtain very different macro behavior.

* NOAH: INSERT 2-3 MORE MERT VIDEOS, WITH CLEAR EXPLANATION OF PARAMETERS EACH TIME

## Streamlining our simulations

Each of the above simulations took several hours to render because simulating and visualizing the movement of tens of thousands of particles over thousands of generations of a reaction-diffusion interaction is computationally intensive. The question is whether we can obtain similar conclusions with a faster model that does not require us to keep track of so many particles. We will turn our attention to this question in the next section.

[Next lesson](blocks){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
