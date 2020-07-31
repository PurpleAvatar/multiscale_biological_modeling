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

The interesting behavior in this system lies in a sweet spot, where we see interesting macro behavior for a given collection of parameters.

For example,

(INSERT MERT VIDEO WITH CLEAR EXPLANATION OF PARAMETERS)

And yet if we make a slight change to the parameters, we obtain very different macro behavior.

(INSERT 2-3 MORE MERT VIDEOS, WITH CLEAR EXPLANATION OF PARAMETERS EACH TIME)

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

[Previous](random-walk){: .btn .btn--primary .btn--x-large} [Next Page](blocks){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
