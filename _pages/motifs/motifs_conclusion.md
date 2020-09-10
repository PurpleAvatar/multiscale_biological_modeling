---
permalink: /motifs/conclusion
title: "Conclusion"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Engineering a repressilator

In *A Synthetic Oscillatory Network of Transcriptional Regulators* by Elowitz and Leibler[^oscillator], the repressilator model we have simulated in CellBlender was successfully tested in a real E. coli cell (an *in vivo* experiment). Instead of the X, Y, Z molecules we used in our simulation, the authors inserted the genes *TetR*, *LacI*, and *cI*. These genes were set up in the same arrangement as our simulation, however there were key differences in the scale of the model. Our simulation was carried out in a single space with approximately 300 molecules per species. The reactions were carried out on the order of around 600 reactions per time step for 120,000 steps. 

![image-center](../assets/images/repressilator_ecoli.png){: .align-center}
The repressilator model used in Elowitz and Leibler's E. coli system
{: style="text-align: center;"}

In contrast, Elowitz and Leibler described a model with a variety of different reaction rates, such as a 0.0005 promoter strength, 20 proteins created per transcript, and a protein half-life of 10 minutes. Interestingly, this scale led to oscillations occurring with a periodicity that spanned different generations of E. coli! Nevertheless, both the real E. coli repressilator systems and our models have shown clear patterns of oscillations with robustness to interruptions and disturbances. We encourage you to further explore these models in the exercises at the end of the chapter.  


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

[^oscillator]: Elowitz, M. B. & Leibler, S. A Synthetic Oscillatory Network of Transcriptional Regulators. Nature 403, 335-338 (2000).