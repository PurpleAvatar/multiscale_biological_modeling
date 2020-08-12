---
permalink: /motifs/conclusion
title: "Conclusion"
sidebar:
 nav: "motifs"
---

## Learning objectives

1. What are motifs?
2. How does the common motif "negative autoregulation" work?
3. How can the motif "feed forward loop" change a cellular response?
4. How can a cell achieve oscillatory behaviors and how robust is this process?

## Notes

* We also need a note at end of chapter about the fact that the cell is growing so that in more robust models the concentration is constantly decreasing as a result of the cell growing since it needs to double its volume every cell cycle.

* What about a link to TF networks of other species? Human? Are these datasets readily available?

* Perhaps define the term "response time"

* Something is missing which is that we could increase the degradation rate as well instead of negative autoregulation. Why do you think that the cell doesn't simply have a higher degradation rate? Why might this be impractical?

* In Noah's second tutorial, Phillip needs to have a question at the end of the tutorial asking the user to draw the conclusion on their own.

* In the results section, should say something about there being practical limitations to how much we can increase the reaction producing *Y*, which provides a trade-off hence why the reaction rate isn't higher.

* (Cite Alon book at some point -- when motifs are introduced? The introduction?)

## Exercises

1. Modify the Jupyter notebook provided in the [tutorial on loops](tutorial_loops) to count the number of feed-forward loops in the transcription factor network for *E. coli.*

2. How many feedforward loops that you found in the preceding exercise are incoherent type-1 feed-forward loops?

3. (Challenge exercise) How many feed-forward loops would you expect to see in a random network having the same number of nodes as the *E. coli* transcription factor network? How does this compare to your answers to the previous two questions?

4. There are eight types of feedforward loops based on the eight different ways in which we can label the edges in the network with a "+" or a "-" based on upregulation or downregulation. Modify the Jupyter notebook to count the number of loops of each type present in the *E. coli* transcription factor network.

* NEED FIGURE HERE showing eight types of network.

[Next chapter](../chemotaxis/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
