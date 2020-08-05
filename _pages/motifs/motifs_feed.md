---
permalink: /motifs/feed
title: "Feed-Forward Loop"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

* The previous section works if we have a transcription factor, but a normal gene is not a transcription factor and therefore is not able to negatively autoregulate.

* The question is how a protein that is not a transcription factor could reach a steady-state concentration faster than with simple regulation, since it can't negatively autoregulate.

* Introduce the feedforward loop. In general, this is any loop in which *X* is connected to both *Y* and *Z*, and then there is an edge connecting *Y* to *Z* as well.

* Note that X and Y must be transcription factors but Z does not have to be (and in fact typically is not).

* Feedforward loops are also a network motif -- we will leave the statistical verification of this as a challenge exercise at the end of the chapter.

* There are eight different types of feed-forward loops depending on the choices of signs on each of the three edges.

* Introduce the type-1 incoherent feed-forward loop. This is a network in which X --> Y and X --> Z but at the same time Y --| Z.

* **STOP:** How could we simulate a feed-forward loop with chemical reactions akin to the simulation we introduced in the previous section?

* Mimicking this FFL with a simulation: let's assume that *X* is at steady-state to begin with, so that we don't need to incorporate its feed/kill.

* We already know how to represent *X* regulating *Y*, which can be achieved with the reaction *X* → *X* + *Y*. Similarly, we will need a reaction *X* → *X* + *Z*.

* Furthermore, we will need to represent degradation of *Y* and *Z* (but not *X* since it is already at steady-state) using the reactions *Y* → *NULL* and *Z* → *NULL*, respectively.

* Finally, recall that in the previous section, we represented the negative autoregulation of a particle *Y* by the reaction 2*Y* → *Y*. In this case, we have negative regulation of *Z* by *Y*. So we have the reaction *Y* + *Z* → *Y* to remove *Z* whenever *Y* and *Z* encounter each other.

* NOAH: this doesn't seem to exactly match what you have in the tutorial where we have additional death rates and hidden particles. Will it still give us similar results?  Why not just assume that *X* is at steady state since it isn't involved in any reactions?  This would be parallel to what we saw in the first section.

* Appeal to tutorial.

[Visit tutorial](tutorial_feed){: .btn .btn--primary .btn--large}

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
