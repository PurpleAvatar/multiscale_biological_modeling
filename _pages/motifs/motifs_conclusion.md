---
permalink: /motifs/conclusion
title: "Conclusion"
sidebar:
 nav: "motifs"
---

## Engineering a repressilator

* NOAH: we need to have an overview of the repressilator experiment from 2000, which apparently was refined in 2016.  Could you give a short overview of how this works here and the extent to which they were able to replicate what we have *in vivo*?

## Looking ahead

* In the next module, we will see that a coarse-grained approach like the one considered in the previous lesson will be vital as we start to build more complicated cellular simulations with many moving parts.

* In fact, we will have so many cellular components and reactions that we will need to completely rethink how we set up our reactions. We hope that you will join us!

* In the meantime, check out the exercises below for some additional challenges on network motifs.

[Next module](../chemotaxis/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Exercises

1. Modify the Jupyter notebook provided in the [tutorial on loops](tutorial_loops) to count the number of feed-forward loops in the transcription factor network for *E. coli.*

2. How many feedforward loops that you found in the preceding exercise are incoherent type-1 feed-forward loops?

3. (Challenge exercise) How many feed-forward loops would you expect to see in a random network having the same number of nodes as the *E. coli* transcription factor network? How does this compare to your answers to the previous two questions?

4. There are eight types of feedforward loops based on the eight different ways in which we can label the edges in the network with a "+" or a "-" based on upregulation or downregulation. Modify the Jupyter notebook to count the number of loops of each type present in the *E. coli* transcription factor network.

![image-center](../assets/images/ffl_types.png){: .align-center}
Types of Feed Forward Loops[^ffl]
{: style="text-align: center;"}

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

* NOAH: should we have an exercise asking students to use NFSim to replicate the other network motifs studied in this module?

![image-center](../assets/images/nf_sim_interrupted_break.PNG){: .align-center}

![image-center](../assets/images/nf_sim_interrupted_long.PNG){: .align-center}

![image-center](../assets/images/nf_sim_interrupted_spike.PNG){: .align-center}


* (Cite Alon book at some point -- when motifs are introduced? The introduction?)

[^ffl]: Image adapted from Mangan, S., & Alon, U. (2003). Structure and function of the feed-forward loop network motif. Proceedings of the National Academy of Sciences of the United States of America, 100(21), 11980–11985. https://doi.org/10.1073/pnas.2133841100