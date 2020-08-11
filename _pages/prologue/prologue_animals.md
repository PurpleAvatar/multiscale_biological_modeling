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

* NOAH: this is where the intro to MCell/CellBlender tutorial link should go I think.

## Changing parameters influence the macro behavior of the reaction-diffusion system

Our plan is to initiate the system with a uniform concentration of *A* particles spread across the grid, and then add a collection of *B* particles to the center of the grid.  But before we do this, we first point out that the results of this simulation may vary depending upon a few things.

A **parameter** is a variable quantity used as input to a model. Parameters are inevitable in biological modeling (and data science in general), and as we will see, changing parameters can cause major changes in the behavior of a system.

Note that there are four parameters relevant to our reaction-diffusion system. Three of these parameters are the feed rate (*f*) of *A* particles, the kill rate of the *B* particles (*k*), and the rate of the predator-prey reaction (*r*). The final parameter of interest corresponds to the diffusion rates of the two types of particle. We report this as a single parameter because the diffusion rates are completely dependent on each other; once the diffusion rate of the *B* particles is set, the diffusion rate of *A* particles will be twice that of the *B* particles.

You can think of all these parameters as dials we can turn, observing how the system changes on the macro level. For example, if we raise the diffusion rate, then the particles will be moving around and bouncing into each other more, which means that we will see more of the reaction *A* + 2*B* → 3*B*.

**STOP:** What will happen as we increase or decrease the feed rate *f*? What about the kill rate *k*?
{: .notice--primary}

For some parameter values, the system is not particularly interesting.  For example, the following animation shows that if *k* is too high, then the *B* particles will die out more quickly than they are replenished by the reaction with *A* particles, and so only *A* particles will be left. In this animation, *A* particles have been colored green and *B* particles have been colored red.

 * NOAH: INSERT VIDEO SHOWING PREY THRIVING AND PREDATORS DYING OUT. Indicate parameters.
<iframe width="640" height="360" src="../assets/mert_predator_dies_f1e1_r5e5.mp4" frameborder="0" allowfullscreen></iframe>
*f* = 10 and *r* = 500,000
{: .text-center}

On the other hand, if *f* is too high, then there will be an increase in the *A* particles. However, there will also be more interactions between *A* particles and pairs of *B* particles, and so we will then see an explosion in the number of predators.

* NOAH: INSERT VIDEO, with parameters indicated)
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

## A reflection on Turing patterns

The Turing patterns that emerge from our animations in the previous section are a testament to the human eye's ability to find organization within the net behavior of tens of thousands of particles.  The patterns are unquestionably there, but they are also quite noisy; this inference of large-scale patterns from small-scale phenomena is in some sense what our brains do best.

What is also remarkable is that the system is so **fine-tuned**, meaning that that very slight changes in parameter values can lead to significant changes in the overall system. In the case of our model, these changes could convert spots to stripes, or they could influence how clearly defined the boundaries of the Turing patterns are.

Much later in this course, we will see an example of a biological system that is the opposite of fine-tuned. In such a **robust** system, variation in the parameters does not lead to substantive changes in the ultimate behavior of the system. Robust processes are vital for processes in which an organism needs to be very resilient to any small changes disturbing some process. We will say more about robustness later.

It turns out that although Turing's work offers a compelling argument for how zebras might have gotten their stripes, the exact mechanism by which these stripes form is still an unresolved question. Although zebras are still up in the air, the pigmentation of *zebrafish* does follow a Turing pattern because two types of pigment cells follow a reaction-diffusion model much like the one we presented above.

CITATION: https://www.pnas.org/content/106/21/8429.

We also have qualitative evidence that the pigmentary patterns arising in fish are due to a fine-tuned system. For example, note that following two photos of giant pufferfish. These fish are genetically very similar, but their skin patterns are very different, with one having spots and the other exhibiting a complex pattern of stripes. What seems like a drastic change in the appearance of the fish can actually be attributable to a small change of parameters in a fine-tuned system that is driven only by random interactions.

(INSERT PUFFERFISH PHOTOS -- https://www.123rf.com/photo_26775011_giant-puffer-fish.html and https://en.wikipedia.org/wiki/File:Giant_Puffer_fish_skin_pattern.JPG or equivalent quality)

## Streamlining our simulations

If you are interested in learning how to generate these simulations on your own computer, please stay tuned. In the next chapter of the course, we will software that can be used to simulate reaction-diffusion interactions and show how it can be used for other forays into biological modeling.

For now, we will point out that each of these simulations took several hours to render on a modern laptop. Visualizing the movement of tens of thousands of particles over thousands of generations of a reaction-diffusion interaction is computationally intensive. The question is whether we can obtain similar conclusions with a faster model that does not require us to keep track of so many particles. We will turn our attention to this question in the next section.

[Next lesson](blocks){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
