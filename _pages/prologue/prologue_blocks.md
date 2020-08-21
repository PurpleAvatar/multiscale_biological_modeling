---
permalink: /prologue/blocks
title: "A Coarse-Grained Turing Pattern Simulation"
sidebar:
 nav: "prologue"
toc: true
toc_sticky: true
---

Although this is an introductory module, there is another maxim of biological modeling that we can convey. To produce and render the animations shown in the previous sections required several hours to run on a powerful laptop using state-of-the-art optimized software that has undergone many revisions over a period of years.

Part of any modeler's work is to see if a simpler model can be found that contains the same essence and replicates the same results but that is capable of being run faster and scaling to larger inputs. For example, imagine how much computational power would be needed to build a particle-based model of your brain; the only way to study such a complicated system is by making simplifications.

In other words, we have a very "fine-grained" reaction-diffusion model illustrating Turing patterns, and we will present a coarser model that allows us to make the same conclusions. To do so, we will stop keeping track of individual particles and instead grid off two-dimensional space into blocks and store only the *concentration* of particles within this block. That is, each block may contain thousands of particles of a given type, but we think of it only as its concentration, represented as a decimal between 0 and 1.

Let us begin with a simple example. Say that we are only considering *A* particles, which are all contained in the central square of our grid. The figure below illustrates the grid, where each square is labeled by its concentration.

* INSERT FIGURE

* IN NEXT ITERATION, WE NEED TO COLOR THIS IMAGE AND EXPLAIN

We will then update this grid after a single time step.



* In this case, we have what is called a fine-grained model of Turing patterns because we are modeling them at the level of individual particles. A “coarser” study of Turing patterns would grid off two-dimensional space into blocks; each block may contain thousands of particles of each type, but we will know quite a lot about this block if we only know the concentration of particles within the block.
* The trick is how to use our particle-based model to build such a discretized block-based model, transitioning each of the rules that we have for how particles interact to describe a system of how blocks change based on their concentrations.
* One famous such discretized model generalizing a reaction-diffusion reaction of two particles is called the Gray Scott model, which we will describe below.

[Next lesson](#){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
