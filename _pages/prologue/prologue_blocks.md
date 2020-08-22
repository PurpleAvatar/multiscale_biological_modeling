---
permalink: /prologue/blocks
title: "The Gray-Scott Model: A Coarse-Grained Turing Pattern Simulation"
sidebar:
 nav: "prologue"
toc: true
toc_sticky: true
---

## The case for a coarse-grained reaction-diffusion model

Although this is an introductory module, there is another maxim of biological modeling that we can convey. To produce and render the animations shown in the previous sections required several hours to run on a powerful laptop using state-of-the-art optimized software that has undergone many revisions over a period of years.

Part of any modeler's work is to see if a simpler model can be found that contains the same essence and replicates the same results but that is capable of being run faster and scaling to larger inputs. For example, imagine how much computational power would be needed to build a particle-based model of your brain; the only way to study such a complicated system is by making simplifications.

In other words, we have a very "fine-grained" reaction-diffusion model illustrating Turing patterns, and we will present a coarser model that allows us to make the same conclusions. To do so, we will stop keeping track of individual particles and instead grid off two-dimensional space into blocks and store only the *concentration* of particles within this block. That is, each block may contain thousands of particles of a given type, but we think of it only as its concentration, represented as a decimal between 0 and 1.

## A cellular model showing diffusion of a single particle

Let us begin with a simple example of the diffusion of a single particle (we can add reactions to this model later). Say that we are only considering *A* particles, which are all contained in the central square of our grid. The figure below illustrates the grid, where each square is labeled by its concentration.

<center>
<img src = "../assets/images/initial_A_concentration.png" width="300">
<figcaption>A 5 x 5 grid showing hypothetical initial concentrations of <em>A</em> particles. Cells are labeled by numbers between 0 and 1 representing their concentration of <em>A</em>. In this example, the central cell has maximum concentration, and no particles are contained in any other cell.</figcaption>
</center>

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

## Slowing down diffusion

There is just one problem. This model of diffusion is too fast! If our model is representing diffusion, then all of the particles would not rush out of the central square in a single time step, only for some of these particles to return in the following time step. Our model is currently too volatile to be reliable as a representation of diffusion.

The solution is to add a parameter <em>d</em><sub><em>A</em></sub> representing the *rate* of diffusion of *A*. Instead of moving a cell's entire concentration of particles to its neighbors in a single time step, we move only the fraction <em>d</em><sub><em>A</em></sub> of them.

So, to revisit our original example, say that <em>d</em><sub><em>A</em></sub> is equal to 0.2. Then after the first time step, only 10% of the central cell's particles will be spread to its neighbors. This means that the central square is updated to 0.9, its adjacent neighbors are updated to 0.2(0.2) = 0.04, and its diagonal neighbors are updated to 0.2(0.05) = 0.01. These values after a single time step are summarized in the figure below.

* INSERT FIGURE

## Adding a second particle to our diffusion simulation

We can adjust the speed of diffusion by adjusting this rate parameter. For example, say that we wish to add particle *B* to the simulation, which also starts with 100% concentration in the central square. Recall that *B*, our "predator" molecule, diffuses half as fast as *A*, the "prey" molecule. If the diffusion rate <em>d</em><sub><em>B</em></sub> is equal to 0.1, then our cells after a time step will be updated as shown in the figure below. This figure represents the concentration of the two particles in each cell as an ordered pair (*a*, *b*), where *a* is the concentration of *A* and *b* is the concentration of *B*.

* INSERT FIGURE

**STOP**: Update the cells in the above figure for the diffusion rates <em>d</em><sub><em>A</em></sub> = 0.2 and <em>d</em><sub><em>B</em></sub> = 0.1.
{: .notice--primary}

We are now ready to implement our model of diffusion and add a visualization to see if our model does a good job of approximating the diffusion process.

* NOAH: link to tutorial on just the diffusion aspect of this.

## Adding reactions and completing the Gray-Scott model

Now that we have established a coarse-grained model for tracking the concentrations of two types of particles as they diffuse in their environment, we will add reactions to the simulation.

Recall that we our reaction-diffusion simulation has three reactions.

1. A "feed" reaction by which new *A* particles are fed into the system at a constant rate.
2. A "death" reaction by which *B* particles are removed from the system at a rate proportional to their current concentration.
3. A "reproduction" reaction *A* + 2*B* → 3*B*.

**STOP**: How might we incorporate these reactions into our coarse-grained model?
{: .notice--primary}

Let us address these reactions one at a time. First, we have the feed rate reaction, which takes place at a **feed rate**. It is tempting to simply add some constant value *f* to the concentration of each cell, but this will cause problems if the concentration is close to 1; we want to avoid a situation in which the feed rate causes the concentration of *A* particles to exceed 1.

Instead, if a given cell has concentration *a*, then we will add *f*(1-*a*) to the concentration of the cell.  For example, if *a* is 0.01, then we will add 0.99*f* to the cell because the current concentration is low. If *a* is 0.8, then we will only add 0.2*f* to the concentration.

* NOAH: thoughts on email in which feed rate isn't quite constant?

Second, we consider the death reaction of *B* particles, which takes place at a **kill rate**. Recall that the death reaction takes place at a rate proportional to the current concentration of *B* particles. As a result, if a cell has concentration *b*, then we will subtract *k* · *b* from its concentration in each step for some constant *k* that is between 0 and 1.

Third, we have the reproduction reaction *A* + 2*B* → 3*B*. The higher the concentration of *A* and *B*, the more this reaction should affect the current concentrations of the two particles. Furthermore, because we need *two* *B* particles in order for the collision to occur, a low concentration of *B* should mean that the reaction is even more rare than if we have a low concentration of *A*. Therefore, if a given cell is represented by the concentrations (*a*, *b*), then we will subtract *a* · *b*<sup>2</sup> from the concentration of *A* and add *a* · *b*<sup>2</sup> to the concentration of *B* in the next time step.

Let us consider an example of how a single cell might update its concentration of both particle types as a result of reaction and diffusion.  Say that we have the following purely hypothetical parameter values:

* <em>d</em><sub><em>A</em></sub> = 0.2
* <em>d</em><sub><em>B</em></sub> = 0.1
* *f* = 0.3
* *k* = 0.4

Furthermore, say that our cell has the concentrations (*a*, *b*) = (0.7, 0.5). Then as a result of diffusion, the cell's concentration of *A* will decrease by 0.7 · <em>d</em><sub><em>A</em></sub> = 0.14, and its concentration of *B* will decrease by 0.5 · 0.1 = 0.05. It will also receive particles from neighboring cells; for example, say that it receives an increase to its concentration of *A* by 0.08 and an increase to its concentration of *B* by 0.06 as the result of diffusion from neighbors.

Now let us consider the three reactions. The feed reaction will cause the cell's concentration of *A* to increase by (1 - 0.7) · *f* = 0.09. The death reaction will cause its concentration of *B* to decrease by 0.5 · *k* = 0.2. And the reproduction reaction will mean that the concentration of *A* decreases by *a* · *b*<sup>2</sup> = 0.175, with the concentration of *B* increasing by the same amount.

As the result of all these processes, we update the concentrations of *A* and *B* to the following values (*a*', *b*') in the next time step.

*a*' = 0.7 - 0.14 + 0.08 + 0.09 - 0.175 = 0.555
*b*' = 0.5 - 0.05 + 0.06 - 0.2 + 0.175 = 0.485

Applying these cell-based reaction-diffusion computations over all cells in parallel and over many generations forms the **Gray-Scott** model. We should now feel confident expanding our previous diffusion tutorial into a model that includes all Gray-Scott reactions. The question is, however, will we still see Turing patterns?

* NOAH: CITE Gray-Scott model original paper.

* NOAH: link to tutorial here

## Reflection on the Gray-Scott model

* This is where we will return from the tutorial and reflect on the different Turing patterns that we can produce at the end of Gray-Scott, perhaps with some embedded GIFs.

[Next lesson](#){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
