---
permalink: /motifs/conclusion
title: "Conclusion"
sidebar:
 nav: "motifs"
---

## A coarse-grained model for reaction-diffusion

* The reaction-diffusion models that we have built in this chapter have noise built into them because they are based on the random movements of particles. In some sense, this is a positive feature of particle-based models, because the consistency of the model's output despite an inherently noisy environment reinforces the robustness of the model.

* However, a downside of the particle model is that it is slow and does not scale well for larger simulations.

* Note that even though the system is ultimately reliant on the interactions of molecules, we are not ultimately interested in the individual particles themselves.  Throughout this module, we have focused only on how the *concentration* of each type of particle changes over time. As in the [prologue](prologue), we could imagine developing a faster, coarser-grained version of the models presented here on network motifs.

* For example, say that we wish to model a degradation reaction. If we start with 10,000 *X* particles, then after a single time step, we can simply subtract some percentage of these particles from the total number; there is no need to generate and keep track of 10,000 particles diffusing.

* Similarly, if we have a removal reaction like *X* + *Y* → *X*, and the diffusion rates of *X* and *Y* are the same, then we may like to assume that the concentrations of *X* and *Y* are uniform; this allows us to subtract some percentage from the concentration of *Y* based on the current concentrations of *X* and *Y*.

* The details of how to build such a coarser-grained model are beyond the scope of our work here, but if you would like to see a tutorial showing how to build particle-free reaction-diffusion simulations corresponding to the models we built throughout this module, check out the tutorial below.

* NOAH: Insert link to NFSim tutorial here.

## Looking ahead

* In fact, in the next module, we will see that a coarse-grained approach will be vital as we start to build more complicated cellular simulations with many moving parts.

* In fact, we will have so many cellular components and reactions that we will need to completely rethink how we set up our reactions. We hope that you will join us!

* In the meantime, check out the exercises below for some additional challenges on network motifs.

[Next module](../chemotaxis/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Exercises

1. Modify the Jupyter notebook provided in the [tutorial on loops](tutorial_loops) to count the number of feed-forward loops in the transcription factor network for *E. coli.*

2. How many feedforward loops that you found in the preceding exercise are incoherent type-1 feed-forward loops?

3. (Challenge exercise) How many feed-forward loops would you expect to see in a random network having the same number of nodes as the *E. coli* transcription factor network? How does this compare to your answers to the previous two questions?

4. There are eight types of feedforward loops based on the eight different ways in which we can label the edges in the network with a "+" or a "-" based on upregulation or downregulation. Modify the Jupyter notebook to count the number of loops of each type present in the *E. coli* transcription factor network.

* NEED FIGURE HERE showing eight types of network.

## Internal notes -- resolve before publication

* We also need a note at end of module about the fact that the cell is growing so that in more robust models the concentration is constantly decreasing as a result of the cell growing since it needs to double its volume every cell cycle.

* What about a link to TF networks of other species? Human? Are these datasets readily available?

* Perhaps define the term "response time"

* Define "activate" and "repress" early on in the module and use these wherever possible instead of upregulate and downregulate.

* Need to cite the origin of the repressilator as a synthetic system -- mention 2000 paper and 2016 paper.

* I wonder what happens in the repressilator if all three particles start out at the same concentration ... will there be enough noise in the system to bounce it into an oscillation?

* Something is missing which is that we could increase the degradation rate as well instead of negative autoregulation. Why do you think that the cell doesn't simply have a higher degradation rate? Why might this be impractical?

* In Noah's second tutorial, Phillip needs to have a question at the end of the tutorial asking the user to draw the conclusion on their own.

* In the results section, should say something about there being practical limitations to how much we can increase the reaction producing *Y*, which provides a trade-off hence why the reaction rate isn't higher.

* (Cite Alon book at some point -- when motifs are introduced? The introduction?)
