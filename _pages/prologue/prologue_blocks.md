---
permalink: /prologue/blocks
title: "A Coarse-Grained Turing Pattern Simulation"
sidebar:
 nav: "prologue"
toc: true
toc_sticky: true
---

## Subsection

Although this is an introductory module, there is another maxim of biological modeling that we can convey. To produce and render the animations shown in the previous sections required several hours to run on a powerful laptop using state-of-the-art optimized software that has undergone many revisions over a period of years.

Part of any modeler's work is to see if a simpler model can be found that contains the same essence and replicates the same results but that is capable of being run faster and scaling to larger inputs. For example, imagine how much computational power would be needed to build a particle-based model of your brain; the only way to study such a complicated system is by making simplifications.

In other words, we have a very "fine-grained" reaction-diffusion model illustrating Turing patterns, and we will present a coarser model that allows us to make the same conclusions. To do so, we will stop keeping track of individual particles and instead grid off two-dimensional space into blocks and store only the *concentration* of particles within this block. That is, each block may contain thousands of particles of a given type, but we think of it only as its concentration, represented as a decimal between 0 and 1.

## Example diffusion of single particle

Let us begin with a simple example of the diffusion of a single particle (we can add reactions to this model later). Say that we are only considering *A* particles, which are all contained in the central square of our grid. The figure below illustrates the grid, where each square is labeled by its concentration.

* INSERT FIGURE

* IN A LATER ITERATION OF THESE FIGURES, WE NEED TO COLOR THIS IMAGE AND EXPLAIN IT

We will then update this grid after a single time step. We will spread out the concentration in each square to its eight neighbors. One way of doing this is to assume that 20% of the current cell's concentration goes to each of its four adjacent neighbors, and that 5% of the cell's concentration goes to its four diagonal neighbors. Because the central square in our ongoing example is the only cell with any particles, after a single time step, the updated concentrations are as shown in the following figure.

* INSERT FIGURE

After an additional time step, we see the particles continue to diffuse to farther neighbors. For example, each diagonal neighbor of the central cell in the above figure, which has a concentration of 0.05, will lose all of its *A* particles in the next step. It will, however, gain 20% of the particles from two of its adjacent neighbors, along with 5% of the particles from the central square. This makes the updated concentration of this cell equal to 0.2(0.2) + 0.2(0.2) = 0.04 + 0.04 = 0.08.

Each of the four cells adjacent to the central square will receive 20% of the particles from two of its adjacent neighbors, which have a concentration of 0.05 each. This cell will also receive 5% of the particles from two of their diagonal neighbors, which have a concentration of 0.2. Therefore, the updated concentration of each of these cells is 0.2(0.05) + 0.05(0.2) = 0.01 + 0.01 = 0.02.

Finally, the central square receives 20% of the particles from each of its four adjacent neighbors, as well as 5% of the particles from each of its four diagonal neighbors. As a result, the central square is updated as 4(0.2)(0.2) + 4(0.05)(0.05) = 0.16 + 0.01 = 0.17.

As a result, the central nine squares after two time steps are as shown in the following figure.

* INSERT FIGURE -- should have ? cells for the cells around the perimeter.

**STOP**: What should the values of the "?" cells be in the above figure? Note that these cells are neighbors of cells with positive concentrations after one time step, so their concentrations should be positive.
{: .notice--primary}

* Have a "click here for answer" with a linked image.

## Subsection

There is just one problem. This model of diffusion is too fast! If our model is representing diffusion, then all of the particles would not rush out of the central square in a single time step, only for some of these particles to return in the following time step. Our model is currently too volatile to be reliable as a representation of diffusion.

The solution is to add a parameter <em>d</em><sub><em>A</em></sub> representing the *rate* of diffusion of *A*. Instead of moving a cell's entire concentration of particles to its neighbors in a single time step, we move only the fraction <em>d</em><sub><em>A</em></sub> of them.

So, to revisit our original example, say that <em>d</em><sub><em>A</em></sub> is equal to 0.1. Then after the first time step, only 10% of the central cell's particles will be spread to its neighbors. This means that the central square is updated to 0.9, its adjacent neighbors are updated to 0.1(0.2) = 0.02, and its diagonal neighbors are updated to 0.1(0.05) = 0.005. These values after a single time step are summarized in the figure below.

* INSERT FIGURE

## Adding a second particle

We can adjust the speed of diffusion by adjusting this rate parameter. For example, say that we add a particle *B* to the simulation, which also starts with 100% concentration in the central square. If the diffusion rate <em>d</em><sub><em>B</em></sub> is equal to 0.2, then our cells after a time step will be shown in the figure below. This figure represents the concentration of the two particles in each cell as an ordered pair.

* INSERT FIGURE

**STOP**: Update the cells in the above figure for the diffusion rates <em>d</em><sub><em>A</em></sub> = 0.1 and <em>d</em><sub><em>B</em></sub> = 0.2.
{: .notice--primary}

We are now ready to implement our model of diffusion and add a visualization to see if this model does a good job of approximating the diffusion process.

* NOAH: link to tutorial on just the diffusion aspect of this.

## New subsection

Now that we can keep track of concentrations of two particles as they spread around their environment, we will add a reaction to the simulation.

* Recall the reaction from the Turing pattern simulation.

* At some point should formally define **Gray-Scott** model.

* Good questions below. May need to be exercises.

**STOP**: Is it ever possible for a square to have a concentration greater than 1? Why or why not?
{: .notice--primary}

**STOP**: Note that the concentrations of all of the particles add up to 1 in each step.
{: .notice--primary}

* In this case, we have what is called a fine-grained model of Turing patterns because we are modeling them at the level of individual particles. A “coarser” study of Turing patterns would grid off two-dimensional space into blocks; each block may contain thousands of particles of each type, but we will know quite a lot about this block if we only know the concentration of particles within the block.
* The trick is how to use our particle-based model to build such a discretized block-based model, transitioning each of the rules that we have for how particles interact to describe a system of how blocks change based on their concentrations.
* One famous such discretized model generalizing a reaction-diffusion reaction of two particles is called the Gray Scott model, which we will describe below.

[Next lesson](#){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
