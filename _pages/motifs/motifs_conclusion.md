---
permalink: /motifs/conclusion
title: "Conclusion: The Importance of Robustness in Biological Oscillations"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## The need for robustness in biological oscillators

Nothing exemplifies the need for robustness in biological systems better than oscillators. If a palpitation causes your heart to skip a beat, it should be able to return quickly to its natural rhythm. If you hold your breath to dive underwater, you shouldn't hyperventilate when you return to the surface. And regardless of what functions your cells perform or what disturbances they find in their environment, they should be able to maintain a normal cell cycle.

An excellent illustration of the robustness of the circadian clock is the body's ability to handle jet lag. There is no apparent reason why humans would have evolved to be resilient to flying halfway around the world. And yet are circadian clock is so resilient that after a few days of fatigue and crankiness, we return to a normal daily cycle.

In the previous lesson, we saw that the repressilator will oscillate even in a noisy environment. This behavior leads us to wonder about the extent to which the repressilator is robust. Much like the circadian clock responding to jet lag, we wonder how quickly the repressilator can respond to the jolt of a sudden disturbance in the concentrations of its particles.

## A coarse-grained model for the repressilator

We have noted that a benefit of using a reaction-diffusion particle model to study network motifs is the inclusion of built-in noise to ensure a measure of robustness. However, as we saw in the [prologue](prologue) with our work on Turing patterns, a downside of a particle-based model is that tracking the movements of many particles leads to a slow simulation that does not scale well given more particles or reactions.

Although our model is ultimately interested in molecular interactions, the conclusions we have made throughout this chapter are only based on the *concentrations* of these particles. Therefore, we might imagine developing a coarser-grained version of our model that allows us to make faster conclusions about particle concentrations without keeping track of the diffusion of individual particles.

For example, say that we are modeling a degradation reaction. If we start with 10,000 *X* particles, then after a single time step, we can simply multiply the number of *X* particles by (1-*r*) where *r* is a parameter related to the rate of the degradation reaction.

As for a repression reaction like *X* + *Y* → *X*, say that the concentrations of *X* and *Y* are uniform throughout the object and the diffusion rates of *X* and *Y* are the same. We can update the concentration of *Y* particles by subtracting some factor times the current concentration of *Y* particles. This factor should be directly related to the current concentrations of both *X* and *Y*.

The technical details behind such a coarse-grained model are beyond the scope of our work in this lesson, but we will return to these technical details in the next module. In the meantime, we provide a tutorial below showing how to build a particle-free simulation replicating the repressilator motif. As part of this tutorial, we will make a major disturbance to the concentration of one of the particles and see how long the disturbance lasts and whether the particle concentrations can resume their oscillations.

[Visit tutorial](tutorial_perturb){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## The repressilator is robust to disturbance

In the figure below, we show a plot of concentrations of each particle in our coarse-gained simulation of the repressilator, with one caveat.  Midway through the simulation, we incorporate a disturbance that causes a spike in the concentration of *Y*.

![image-center](../assets/images/nf_sim_interrupted.PNG){: .align-center}
Adding a significant number of *Y* particles to our simulation produces little ultimate disturbance to the concentrations of the three particles, which return to normal oscillations within a single cycle.
{: style="font-size: medium;"}

Because of the spike in the concentration of *Y*, the reaction *Y* + *Z* → *Y* suppresses the concentration of *Z* for longer than usual, and so the concentration of *X* is free to increase for longer than normal. As a result, the next peak in the concentration of *X* is higher than normal.

We might hypothesize that this process would continue, with a tall peak in the concentration of *Z*. However, the peak in the concentration of *Z* is no taller than normal, and the next peak shows a normal concentration of *X*. In other words, the system has very quickly absorbed the blow of an increase in concentration of *Y* and returned to normal within one cycle.

The repressilator happens to be particularly successful at stabilizing. While there have been some attempts to study what makes oscillators robust, the process remains difficult to describe. By characterizing the number and type of interactions within the oscillator model, it has been shown that about 5 reactions minimum are needed for a very robust oscillator[^repress]. The symmetrical nature of the repressilator model may also contribute to its robustness.

In fact, even with a much larger jolt to the repressilator, we observe the concentrations of the three particles return to normal oscillations very quickly.

![image-center](../assets/images/nf_sim_interrupted_spike.PNG){: .align-center}

The repressilator is not the only network motif that leads to oscillations in particle concentrations, but robustness to disturbances in these concentrations is a shared feature of all these motifs.

The robustness of our repressilator model also implies a bigger picture moral in biological modeling. If an underlying biological system demonstrates robustness to change, then any model of that system should also be able to withstand this change. Conversely, we should be wary of any model of a robust system that is overly sensitive to changes in the system.

In this module, we have seen that even very simple network motifs can have a powerful effect on a cell's ability to implement elegant systems of behavior. In the next module, we will encounter a much more involved biochemical process, with far more molecules and reactions, that is used by bacteria to cleverly (and robustly) explore their environment. In fact, we will have so many reactions that we will need to rethink how we set up our model. We hope that you will join us!

In the meantime, check out the exercises below to continue developing your understanding of how transcription factor network motifs have evolved.

## Engineering a repressilator

In *A Synthetic Oscillatory Network of Transcriptional Regulators* by Elowitz and Leibler[^oscillator], the repressilator model we have simulated in CellBlender was successfully tested in a real E. coli cell (an *in vivo* experiment). Instead of the X, Y, Z molecules we used in our simulation, the authors inserted the genes *TetR*, *LacI*, and *cI*. These genes were set up in the same arrangement as our simulation, however there were key differences in the scale of the model. Our simulation was carried out in a single space with approximately 300 molecules per species. The reactions were carried out on the order of around 600 reactions per time step for 120,000 steps.

![image-center](../assets/images/repressilator_ecoli.png){: .align-center}
The repressilator model used in Elowitz and Leibler's *E. coli* system.
{: style="text-align: center;"}

In contrast, Elowitz and Leibler described a model with a variety of different reaction rates, such as a 0.0005 promoter strength, 20 proteins created per transcript, and a protein half-life of 10 minutes. Interestingly, this scale led to oscillations occurring with a periodicity that spanned different generations of E. coli! Nevertheless, the real E. coli repressilator systems showed clear patterns of oscillations with robustness to interruptions and disturbances. How would our simulations hold up to interruptions, and why is this kind of behavior needed in oscillators?   

## Looking ahead

* In the next module, we will see that a coarse-grained approach like the one considered in the previous lesson will be vital as we start to build more complicated cellular simulations with many moving parts.

* In fact, we will have so many cellular components and reactions that we will need to completely rethink how we set up our reactions. We hope that you will join us!

* In the meantime, check out the exercises below for some additional challenges on network motifs.

[Visit Exercises](exercises){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


[^ffl]: Image adapted from Mangan, S., & Alon, U. (2003). Structure and function of the feed-forward loop network motif. Proceedings of the National Academy of Sciences of the United States of America, 100(21), 11980–11985. https://doi.org/10.1073/pnas.2133841100

[^oscillator]: Elowitz, M. B. & Leibler, S. A Synthetic Oscillatory Network of Transcriptional Regulators. Nature 403, 335-338 (2000).

[^repress]: Castillo-Hair, S. M., Villota, E. R., & Coronado, A. M. (2015). Design principles for robust oscillatory behavior. Systems and Synthetic Biology, 9(3), 125–133. https://doi.org/10.1007/s11693-015-9178-6
