---
permalink: /motifs/exercises
title: "Exercises for Exploring Motifs"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---


## Exercises

1. Modify the Jupyter notebook provided in the [tutorial on loops](tutorial_loops) to count the number of feed-forward loops in the transcription factor network for *E. coli.*

2. How many feedforward loops that you found in the preceding exercise are incoherent type-1 feed-forward loops?

3. (Challenge exercise) How many feed-forward loops would you expect to see in a random network having the same number of nodes as the *E. coli* transcription factor network? How does this compare to your answers to the previous two questions?

4. There are eight types of feedforward loops based on the eight different ways in which we can label the edges in the network with a "+" or a "-" based on upregulation or downregulation. Modify the Jupyter notebook to count the number of loops of each type present in the *E. coli* transcription factor network.

![image-center](../assets/images/ffl_types.png){: .align-center}
Types of Feed Forward Loops[^ffl]
{: style="text-align: center;"}

5. More complex motifs may require more computational power to discover. Can you modify the Jupyter Notebook to identify circular loops of transcription factor regulation, such as the multi-component loop below?

![image-center](../assets/images/s_cerevisiae_tf_network.jpg){: .align-center}
Example of different motifs within the *S. Cerevisiae* network[^scNetwork]
{: style="text-align: center;"}

6. Using the *NAR_comparison_equal.blend* file from the NAR Tutorial, increase the reaction rate of X1 -> X1 + Y1 to 4e4, so the table should now look like:

| Reactants |Products|Forward Rate|
|:--------|:-------:|--------:|
| X1’  | X1’ + Y1’ | 4e5 |
| X2’  | X2’ + Y2’ | 4e2 |
| Y1’  | NULL | 4e2 |
| Y2’  | NULL | 4e2 |
|Y2’ + Y2’|Y2’|4e2|

If we plot this graph, we can see the steady states of Y1 and Y2 are different once again. Can you repair the system to find the appropriate reaction rate for X2 -> X2 + Y2 to make the steady states equal once more? Are you about to adjust the reaction Y2 + Y2 -> Y2 as well? Do the reaction rates scale at the same rate?

## Internal notes -- resolve before publication

* We also need a note at end of module about the fact that the cell is growing so that in more robust models the concentration is constantly decreasing as a result of the cell growing since it needs to double its volume every cell cycle.

* Exercise: develop a version of Gray-Scott from prologue that mimics the repressilator (?)

* What about a link to TF networks of other species? Human? Are these datasets readily available?

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

[Next module](../chemotaxis/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
