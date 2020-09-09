---
permalink: /motifs/feed
title: "The Feedforward Loop Motif"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Feedforward loops

In the previous section, we saw that negative autoregulation can be used to speed up response times of a protein to an external stimulus.  However, the catch is that negative autoregulation can only occur if the protein in question is itself a transcription factor. Only about 300 out of 4,400 total *E. coli* proteins are transcription factors[^tfNumber]. So is there a simple way of speeding up a cell's ability to manufacture a protein if that protein is not a transcription factor?

The answer will lie in a small network motif called the **feedforward loop**, which we will call an **FFL**. Earlier in the chapter, we pointed out that negative autoregulation is an example of "feedback", since a transcription factor is involved in regulating its own production. The feedforward loop motif, shown in the figure below, is any loop in which *X* is connected to both *Y* and *Z*, and *Y* is connected to *Z*. In this sense, calling the FFL motif a "loop" is a misnomer. Rather, it is a small structure in which there are two "paths" from *X* to *Z*; one via direct regulation of *Z* by *X*, and another in which there is an intermediate transcription factor *Y*.

<center>
<img src="../assets/images/feed-forward_loop.png" width="300">
<figcaption>The feedforward loop motif. *X* regulates both *Y* and *Z*, and *Y* regulates *Z*.</figcaption>
</center>

<br>
Note that *X* and *Y* must be transcription factors, but *X* does not have to be (and in fact typically is not). There are about 42 FFLs in the transcription factor network of *E. coli*, and we leave the verification that this is a significant number of FFLs compared to a random network as an exercise at the end of the chapter[^ffl].

Furthermore, recall that every edge of a transcription factor network is assigned a "+" or a "-" sign based on whether the interaction corresponds to up-regulation or down-regulation. Accordingly, there are eight different types of FFLs, depending on the labels of the three edges in this motif.

Among the 42 total FFLs in the *E. coli* transcription factor network, 5 of them have the structure below, in which the edges connecting *X* to *Y* and *X* to *Z* are assigned a "+" and the edge connecting *Y* to *Z* is assigned a "-". This specific form of the FFL motif is unfortunately named a **type-1 incoherent feedforward loop**. This form of the FFL will be our focus for the rest of the chapter.

**STOP:** How could we simulate a feedforward loop with chemical reactions akin to the simulation that we used for negative autoregulation? What would we compare this simulation against?
{: .notice--primary}

<center>
<img src="../assets/images/type-1_incoherent_feed-forward_loop.png" width="300">
<figcaption>The incoherent feed-forward loop network motif. Note that *X* upregulates *Y* and *Z*, while *Y* downregulates *Z*.</figcaption>
</center>

## Modeling a type-1 incoherent feedforward loop

As we did in the last section, we will run two simulations. In the first, we will have a simple upregulation of *Z* by *X*, meaning that we will assume *X* is at its steady state concentration and that *Z* is produced by the reaction *X* → *X* + *Z* and removed by the reaction *Z* → *NULL*.

The second simulation will include all of these reactions, but we will also have the reaction *X* → *X* + *Y* to model the upregulation of *Y* by *X*, along with the reaction *Y* + *Z* → *Y* to model the downregulation of *Z* by *Y*. Because *Y* is being produced as the result of a reaction, we will also have a reaction *Y* → *NULL* to model the degradation of *Y*. For the sake of fairness, we will have the same degradation rates for both *Y* and *Z*.

Furthermore, in order to obtain a mathematically controlled comparison, we will need to make the reaction *X* → *X* + *Z* have a higher rate in the second simulation modeling the FFL. Without raising the rate of this reaction, the downregulation of *Z* by *Y* will cause the steady state concentration of *Z* to be lower in the FFL simulation.

If you are feeling adventurous, you may like to adapt the [NAR tutorial](motifs_tutorial_nar) to run these two simulations and tweak the rate of the *X* → *X* + *Z* reaction to see if you can obtain the same steady state concentration of *Z* in the two simulations and observe the results. We also provide the following tutorial walking you through setting up the simulations.

[Visit tutorial](tutorial_feed){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Why feedforward loops speed up response times

In the figure below, we show a plot visualizing the amount of *Z* across the two simulations. As with negative autoregulation, we see that the type-1 incoherent FFL allows the cell to ramp up production of a gene *Z* to steady state much faster than it would under simple regulation.

![image-center](../assets/images/ffl_graph.PNG){: .align-center}
In dark purple we see the results of a FFL compared with light blue showing a normal steady state reaction
{: style="text-align: center;"}

However, you will note a slightly different pattern to the growth of *Z* than we saw under negative autoregulation. In negative autoregulation, the concentration of the protein approached steady state from below. In the case of the FFL, the amount of *Z* grows so quickly that it passes its steady state and later returns to steady state from above.

We can interpret from the model why the FFL allows for a fast growth to steady state as well as why it initially passes the steady state concentration. At the start of the simulation, *Z* is upregulated by *X* very quickly.

*X* regulates the production of *Y* as well, but at a lower rate than the regulation of *Z* because *Y* only has its own degradation to slow this process. Therefore, more *Z* is initially produced than *Y*.

As the concentration of *Y* builds up, it starts to downregulate *Z*. The more *Y* we have, and the more *Z* that we have, the more often the reaction *Y* + *Z* → *Y* will occur. Because the amounts of both *Y* and *Z* increase over time, this reaction serves as the "brakes" for the concentration of *Z*; these brakes need to be very powerful because the concentration of *Z* is growing faster than that of *Y*, the transcription factor downregulating it.

## Summary

To conclude our work with FFLs, we note that the feedforward process must be vital to the cell. Unlike negative autoregulation, the FFL requires two separate transcription factors working together in order to increase the production of our target gene.

We only considered one of the eight types of FFL in this section. You might wonder whether there are other FFL structures that serve as network motifs.  For example, what purpose might it serve if *X* downregulates *Y* and *Y* upregulates *Z*? We will explore these additional FFL structures in the exercises at the end of the chapter.

Finally, we return to the figure above, in which we saw that the concentration of *Z* swung past its steady state before returning to the steady state. This figure offers a sort of **damped oscillation** process in which the concentration of a particle alternates between being above and below its steady state, while the amplitude of the oscillation gets smaller and smaller.

This process is very similar to a true oscillation, in which the concentration of the particle bounces back and forth around a steady state concentration, but these oscillations neither "dampen" over time nor grow out of control. The question is what kind of network motif might produce oscillatory behavior without needing outside influence to the system, and how such a motif might be useful. We will explore such a motif and its applications in the next section.

[Next lesson](oscillators){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^tfNumber]: According to the Gene ontology (biological process)
"search for trasncription" https://www.uniprot.org/

[^ffl]: Mangan, S., & Alon, U. (2003). Structure and function of the feed-forward loop network motif. Proceedings of the National Academy of Sciences of the United States of America, 100(21), 11980–11985. https://doi.org/10.1073/pnas.2133841100
