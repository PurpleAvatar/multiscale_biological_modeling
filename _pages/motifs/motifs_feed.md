---
permalink: /motifs/feed
title: "Feed-Forward Loop"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Feedforward loops

In the previous section, we saw that negative autoregulation can be used to speed up response times of a protein to an external stimulus.  However, the catch is that negative autoregulation can only occur if the protein in question is itself a transcription factor. Only XXX out of YYY total *E. coli* proteins are transcription factors. So is there a simple way of speeding up a cell's ability to manufacture a protein if that protein is not a transcription factor?

* NOAH: Fill in XXX and YYY above.

The answer will lie in a small network motif called the **feedforward loop**, which we will call an **FFL**. Earlier in the chapter, we pointed out that negative autoregulation is an example of "feedback", since a transcription factor is involved in regulating its own production. The feedforward loop motif, shown in the figure below, is any loop in which *X* is connected to both *Y* and *Z*, and *Y* is connected to *Z*. In this sense, calling the FFL motif a "loop" is a misnomer. Rather, it is a small structure in which there are two "paths" from *X* to *Z*; one via direct regulation of *Z* by *X*, and another in which there is an intermediate transcription factor *Y*.

* INSERT FIGURE HERE SHOWING FEEDFORWARD LOOP

Note that *X* and *Y* must be transcription factors, but *X* does not have to be (and in fact typically is not). There are XXX FFLs in the transcription factor network of *E. coli*, and we leave the verification that this is a significant number of FFLs compared to a random network as an exercise at the end of the chapter.

* NOAH: Fill in this XXX above.

Furthermore, recall that every edge of a transcription factor network is assigned a "+" or a "-" sign based on whether the interaction corresponds to up-regulation or down-regulation. Accordingly, the figure below shows the eight different types of FFLs, depending on the signs labeling the three edges in the FFL.

* FILL IN FIGURE WITH EIGHT DIFFERENT TYPES OF FFLs

Among the XXX total FFLs in the *E. coli* transcription factor network, YYY of them have the structure below, in which the edges connecting *X* to *Y* and *X* to *Z* are assigned a "+" and the edge connecting *Y* to *Z* is assigned a "-". This specific form of the FFL motif is unfortunately named a **type-1 incoherent feedforward loop**. This form of the FFL will be our focus for the rest of the chapter.

* NOAH: Fill in XXX and YYY here.

* FILL IN FIGURE WITH TYPE-1 INCOHERENT FFL.

**STOP:** How could we simulate a feed-forward loop with chemical reactions akin to the simulation that we used for negative autoregulation? What would we compare this simulation against?

## Modeling a type-1 incoherent feedforward loop

* Mimicking this FFL with a simulation: let's assume that *X* is at steady-state to begin with, so that we don't need to incorporate its feed/kill.

* We already know how to represent *X* regulating *Y*, which can be achieved with the reaction *X* → *X* + *Y*. Similarly, we will need a reaction *X* → *X* + *Z*.

* Furthermore, we will need to represent degradation of *Y* and *Z* (but not *X* since it is already at steady-state) using the reactions *Y* → *NULL* and *Z* → *NULL*, respectively.

* Finally, recall that in the previous section, we represented the negative autoregulation of a particle *Y* by the reaction 2*Y* → *Y*. In this case, we have negative regulation of *Z* by *Y*. So we have the reaction *Y* + *Z* → *Y* to remove *Z* whenever *Y* and *Z* encounter each other.

* NOAH: this doesn't seem to exactly match what you have in the tutorial where we have additional death rates and hidden particles. Will it still give us similar results?  Why not just assume that *X* is at steady state since it isn't involved in any reactions?  This would be parallel to what we saw in the first section.

* Appeal to tutorial.

[Visit tutorial](tutorial_feed){: .btn .btn--primary .btn--large}

## Why feedforward loops speed up response times

* Explanation as to why this might be faster than simple regulation of *Z* by *X*. When we start the simulation, *Z* gets upregulated by *X*, at a higher rate than it would under simple regulation.

* *X* regulates *Y* as well. As the concentration of *Y* builds up, it starts to downregulate *Z*. The more *Y* we have, and the more *Z* that we have, the more of the reaction *Y* + *Z* → *Y* we will see. Because *Y* and *Z* are increasing over time, this reaction serves as the "brakes" for the reaction increasing the quantity of *Z* present.

* Returning from the tutorial, let us examine a plot of *Z* for the feed-forward loop compared against a simple regulation of *Z* by *X*.

* Need to make sure that it's clear that the simulation causes the concentration of *Z* to actually pass the steady state before it returns back to the starting point.

* Important point to be made is that it is clear that this is an important motif to the cell because it requires two transcription factors in some sense working together in order to increase the production of *Z* faster.

* Possible transition to the next lesson: in this simulation we saw that the concentration of the particle of interest passed its steady state and then was driven back down to the steady state. Contrast this with negative autoregulation, in which the concentration of the particle of interest simply approached the steady-state from beneath.

* Need a connection to an oscillator -- would it be possible for the concentration of the particle of interest to swing back beneath steady state, then above steady state again, and so on, so that a steady state was not reached but in fact the system converged to oscillating behavior?

* Point to next lesson, where we will discuss a model for oscillation, an ubiquitous aspect of biological systems.

[Next lesson](oscillators){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
