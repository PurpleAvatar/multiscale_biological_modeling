---
permalink: /prologue/blocks
title: "A Coarse-Grained Turing Pattern Simulation"
sidebar:
 nav: "prologue"
toc: true
toc_sticky: true
---

* There is another maxim of biological modeling at hand.  To produce and render the animations shown in the previous sections of XXX particles over YYY generations required several hours on a powerful computer using state-of-the-art software.
* If you have time and would like to run these animations yourself, we will provide tutorials in a later module of the course when we discuss this software, called CellBlender, and apply it in the context of a different biological modeling problem. So stay tuned ?
* But for now, we point out that part of the modeller’s work is to see if a model can be replicated using an even simpler model that provides the same conclusions faster and more clearly.  For example, although for this simple example we were able to observe Turing patterns emerge from a particle-based simulation, more sophisticated models will require more and more computational power. Imagine how much computational power would be needed to build an accurate model of your brain on the particle level!
* In this case, we have what is called a fine-grained model of Turing patterns because we are modeling them at the level of individual particles. A “coarser” study of Turing patterns would grid off two-dimensional space into blocks; each block may contain thousands of particles of each type, but we will know quite a lot about this block if we only know the concentration of particles within the block.
* The trick is how to use our particle-based model to build such a discretized block-based model, transitioning each of the rules that we have for how particles interact to describe a system of how blocks change based on their concentrations.
* One famous such discretized model generalizing a reaction-diffusion reaction of two particles is called the Gray Scott model, which we will describe below.

[Next lesson](#){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
