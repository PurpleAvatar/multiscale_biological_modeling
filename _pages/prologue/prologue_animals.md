---
permalink: /prologue/animals
title: "A Reaction-Diffusion Model and Turing Patterns"
sidebar:
 nav: "prologue"
toc: true
toc_sticky: true
---

## From random walks to reaction-diffusion

In the previous section, we introduced the random walk model of a particle diffusing through a medium as a result of Brownian motion. But what exactly does the random movement of particles have to do with Alan Turing and zebras?

Turing's insight was that remarkable patterns could emerge if we combine a simulation of diffusion with a chemical reaction, in which colliding particles interact with each other. Such a model is called a **reaction-diffusion system**, and the patterns that emerge in the simulation are called **Turing patterns** in Turing's honor.

## An example reaction-diffusion system

We will consider a reaction-diffusion system having two types of particles, *A* and *B*. The system is not meant to represent a predator-prey relationship, but you may like to think of the *A* particles as prey and the *B* particles as predators for reasons that will become clear soon.

Both types of particles diffuse randomly through the plane, but the *A* particles typically diffuse more quickly than the *B* particles.  In the simulation that follows, we will assume that *A* particles diffuse twice as quickly as *B* particles. In terms of the random walk, this faster rate of Brownian motion means that in a single "step", an *A* particle moves twice as far as a *B* particle.

**STOP**: Say that we release one *A* particle and one *B* particle at the same location. If the two particles move via random walks, and the rate of diffusion of *A* is twice as fast, then how much farther from the origin will *A* be than *B* after *n* steps?
{: .notice--primary}

We now will add some reactions to our system. The *A* particles are added into the system at some constant **feed rate** *f*, meaning that these particles are created as the result of other reactions that are not part of our model. In a three-dimensional system, the units of *f* are in mol/L/s, which means that every second, there are *f* moles of particles added to the system in every liter of volume. (Recall from your chemistry class long ago that one mole is 6.02214076 · 10<sup>23</sup> particles.) As a result, the concentration of the particles increases by a constant number in each time step.

There is also a **kill rate** constant *k* dictating the rate of removal of the *B* particles. As a result of removal, the number of *B* particles in the system will decrease by a factor of *k* in a given time step. That is, the more *B* particles that are present, the more *B* particles will be removed.

Note that there is a slight difference between the feed and kill reactions. In the first reaction, the number of *A* particles increases by a constant number in each time step. In the second reaction, the number of *B* particles decreases by a constant factor multiplied by the current number of *B* particles. In terms of calculus, this means that if [*A*] and [*B*] denote the concentrations of the two particle types, then in the absence of other reactions, we can write

<center>
<em>d[A]</em>/<em>dt</em> = <em>f</em>
</center>

and

<center>
<em>d[B]</em>/<em>dt</em> = -<em>k</em> · <em>[B]</em>.
</center>

Finally, this reaction-diffusion system has a single reaction of the two particles with each other. If an *A* particle and two *B* particles encounter each other, then the *A* particle is replaced by a third *B* particle at a certain rate *r*. This reaction can be summarized by the following chemical reaction.

<p><center><em>A</em> + 2<em>B</em> → 3<em>B</em></center></p>

This reaction is why we compared *A* to prey and *B* to predators, since we can imagine this reaction as two *B* particles consuming an *A* particle and conceiving an offspring *B* particle. Another way of viewing this reaction is that when an *A* particle and two *B* particles encounter each other, the reaction takes place with probability proportional to *r*.

## MCell and Simulations

The software MCell and other **particle-based spatial stochastic simulation** methods keep track of several factors which create our model. Firstly, the trajectories of individual particles are tracked to predict movement, introduce random diffusion, and detect collisions. When a collision occurs, particles can undergo reactions which are specified by the user. Our typical reaction rate, which may describe a reaction like:

<center><em>A</em> + 2<em>B</em> → 3<em>B</em><br></center>

The reaction rate we use in this equation describes the **bulk reaction rate**, or the total number of reactions occuring depending on the concentrations of reactants. Because MCell needs to only have bimolecular reactions occur when a collision occurs, the user will give MCell the bulk reaction rate and MCell will automatically choose a probability of reaction per collision based on how many collisions are expected in order to match the bulk reaction rate.  

[Visit Tutorial](tutorial-diffusion){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Changing parameters influence the macro behavior of the reaction-diffusion system

Our plan is to initiate the system with a uniform concentration of *A* particles spread across the grid, and then add a collection of *B* particles to the center of the grid.  But before we do this, we first point out that the results of this simulation may vary depending upon a few things.

A **parameter** is a variable quantity used as input to a model. Parameters are inevitable in biological modeling (and data science in general), and as we will see, changing parameters can cause major changes in the behavior of a system.

Note that there are four parameters relevant to our reaction-diffusion system. Three of these parameters are the feed rate (*f*) of *A* particles, the kill rate of the *B* particles (*k*), and the rate of the predator-prey reaction (*r*). The final parameter of interest corresponds to the diffusion rates of the two types of particle. We report this as a single parameter because the diffusion rates are completely dependent on each other; once the diffusion rate of the *B* particles is set, the diffusion rate of *A* particles will be twice that of the *B* particles.

You can think of all these parameters as dials we can turn, observing how the system changes on the macro level. For example, if we raise the diffusion rate, then the particles will be moving around and bouncing into each other more, which means that we will see more of the reaction *A* + 2*B* → 3*B*.

**STOP:** What will happen as we increase or decrease the feed rate *f*? What about the kill rate *k*?
{: .notice--primary}

For some parameter values, the system is not particularly interesting.  For example, the following animation is produced for *k* = 500,000 and *f* = 10. It shows that if *k* is too high, then the *B* particles will die out more quickly than they are replenished by the reaction with *A* particles, and so only *A* particles will be left. In this animation, *A* particles have been colored green, and *B* particles have been colored red.

<iframe width="640" height="360" src="../assets/mert_predator_dies_f1e1_r5e5.mp4" frameborder="0" allowfullscreen></iframe>
Predators dying out quickly, Feed Rate *f* = 1E1 and Kill Rate *k* = 5E5
{: .text-center}

On the other hand, if *f* is too high, then there will be an increase in the *A* particles. However, there will also be more interactions between *A* particles and pairs of *B* particles, and so we will then see an explosion in the number of predators.

<iframe width="640" height="360" src="../assets/mert_f1e6_d1e5.mp4" frameborder="0" allowfullscreen></iframe>
Predators overtaking prey due to excess of prey, Feed Rate *f* = 1E4 and Kill Rate *k* = 1E5
{: .text-center}

The interesting behavior in this system lies in a sweet spot, where we see interesting macro behavior for a given collection of parameters.

Let's scale up the simulation! With more particles and larger simulation space, we will be able to observe larger patterns. For example,

<iframe width="640" height="360" src="../assets/gray_scott_11_by_11_f_1.75_k_2_new.mp4" frameborder="0" allowfullscreen></iframe>
A fizzling cascade bounces in between larger waves, Feed Rate *f* = 1.75E5 and Kill Rate *k* = 2E5
{: .text-center}

And yet if we make a slight change to the parameters, we obtain different macro behavior.

<iframe width="640" height="360" src="../assets/gray_scott_11_by_11_f_1.4_k_2.mp4" frameborder="0" allowfullscreen></iframe>
Each ripple is started by a small spiral, Feed Rate *f* = 1.4E5 and Kill Rate *k* = 2E5
{: .text-center}

<iframe width="640" height="360" src="../assets/gray_scott_11_by_11_f_1_k_1.mp4" frameborder="0" allowfullscreen></iframe>
When we push the feed even lower, we see much cleaner waves, Feed Rate *f* = 1E5 and Kill Rate *k* = 2E5
{: .text-center}

<iframe width="640" height="360" src="../assets/gray_scott_11_by_11_f_1_k_2.mp4" frameborder="0" allowfullscreen></iframe>
Pushing the kill rate down as well leads to a spotty pattern (pause the video at various points for a clear look), Feed Rate *f* = 1E5 and Kill Rate *k* = 1E5
{: .text-center}

## Turing patterns and hallucinations

When you look at the simulations above, an adjective that may have come to mind is  "trippy". This is no accident. Research dating all the way back to the 1920s has studied the patterns that we see when we hallucinate, which Heinrich Klüver named **form constants** after studying patients who had taken mescaline.[^kluver] Form constants, which include cobwebs, tunnels, and spirals, occur across many individuals regardless of the cause of the hallucinations.

Over five decades after Klüver's work, researchers would determine that form constants with seemingly different shapes originate from simpler *linear* patterns of cellular activation in the retina. Because the retina is circular, the brain needs to convert this cellular image into a rectangular field of view; as a result, when the linear patterns are passed to the visual cortex, the brain contorts them into the form constants that we see.[^cowan]

Yet this work had replaced one question with another: why does hallucination cause patterns of cellular activation in the retina? This question is still unresolved, but some researchers[^quanta] believe that these patterns are in fact Turing patterns and can be explained by a reaction-diffusion model similar to the one that we have considered in this chapter.

## Streamlining our simulations

Each of the above simulations took several hours to render because simulating and visualizing the movement of tens of thousands of particles over thousands of generations of a reaction-diffusion interaction is computationally intensive. The question is whether we can obtain similar conclusions with a faster model that does not require us to keep track of so many particles. We will turn our attention to this question in the next section.

[Next lesson](blocks){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^cowan]: G.B. Ermentrout and J.D. Cowan. "A Mathematical Theory of Visual Hallucination Patterns". *Biol. Cybernetics* 34, 137-150 (1979).

[^kluver]: H. Klüver. *Mescal and Mechanisms of Hallucinations*. University of Chicago Press, 1966.

[^quanta]: J. Ouellette. "A Math Theory for Why People Hallucinate". *Quanta Magazine*, July 30, 2018. https://www.quantamagazine.org/a-math-theory-for-why-people-hallucinate-20180730/
