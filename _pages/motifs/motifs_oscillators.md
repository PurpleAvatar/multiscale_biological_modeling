---
permalink: /motifs/oscillators
title: "Building a Biological Oscillator"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Oscillators are everywhere in nature

Even if placed in a bunker, humans will maintain a roughly 24-hour cycle of sleep and wakefulness. However, such a **circadian rhythm** is not unique to humans or even animals but rather is present throughout living things, including plants and even cyanobacteria.

* NOAH: cite the bunker experiment: Aschoff, J. (1965). Circadian rhythms in man. Science 148, 1427–1432.

* NOAH: also cite the first paper that found circadian rhythm in cyanobacteria: Grobbelaar N, Huang TC, Lin HY, Chow TJ. 1986. Dinitrogen-fixing endogenous rhythm in Synechococcus RF-1. FEMS Microbiol Lett 37:173–177. doi:10.1111/j.1574-6968.1986.tb01788.x.CrossRefWeb of Science.

Life processes like the circadian rhythm that **oscillate** between different states are not confined to circadian rhythms. You may feel like you have some control over when you go to bed, but your heart and respiratory system both follow cyclical rhythms without you even thinking about it. On a much lower level, eukaryotic cells are governed by a strict cell cycle as the cells grows and divide.

We know that there is no intelligence that drives all these cyclic processes, and we might guess from what we have learned in this module that they must be built upon simple rules serving as a **pacemaker** controlling the oscillations. However, the question remains as to what these pacemakers are.

We also suspect that these rhythms also must be *robust*. That is, they should be resilient to small changes in order to be executed correctly many times over an organism's life. But how is this robustness achieved?

## The repressilator: a synthetic biological oscillator

Researchers have identified many network motifs that facilitate oscillation, some of which are very complicated and include many components. In this lesson, we will focus on a simple three-component oscillator motif called a **repressilator**. We will implement the repressilator with a particle simulator but also then analyze the robustness of this system in response to small changes in concentrations of particles.

* CITE repressilator.

The repressilator motif is shown in the figure below. In this motif, all three proteins are transcription factors, and they form a cycle in which *X* represses *Y*, *Y* represses *Z*, and *Z* represses *X* (hence the name). The repressilator clearly forms a feedback loop, but nothing *a priori* about this motif would indicate that it would lead to oscillation; after all, we have already seen feedback processes in this module that did not lead to oscillation.

<center>
<img src="../assets/images/repressilator.png" width="250">
<figcaption>The repressilator motif for three particles <em>X</em>, <em>Y</em>, and <em>Z</em>. <em>X</em> represses <em>Y</em>, which represses <em>Z</em>, which in turn represses <em>X</em>, forming a feedback loop.</figcaption>
</center>

**STOP:** Try building a reaction-diffusion model for the repressilator, assuming that we start with an initial concentration of *X* and no *Y* or *Z* particles.
{: .notice--primary}

## Modeling a repressilator with a reaction-diffusion particle simulation

To build a reaction-diffusion model accompanying the repressilator, we start with a quantity of *X* particles, and no *Y* or *Z* particles. We then assume that all three particles diffuse at the same rate and degrade at the same rate.

Furthermore, we assume that all three particles are produced as the result of an activation process by some other transcription factor(s), which we assume happens at the same rate. We will use a single type of particle *I* that will be hidden and serves to activate the three visible particles by the reactions *I* → *I* + *X*, *I* → *I* + *Y*, and *I* → *I* + *Z*.

In the previous lesson on the feed-forward loop, we saw that to model a repression of *Y* by *X*, we can use the reaction *X* + *Y* → *X*. We combine this reaction with the additional two reactions *Y* + *Z* → *Y*, and *Z* + *X* → *Z* to complete the repressilator model.

If you have followed our previous tutorials, then you may feel comfortable taking off the training wheels and trying out implementing the repressilator on your own. We also are more than happy to provide a tutorial if you find it useful.

[Visit tutorial](tutorial_oscillators){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Interpreting the repressilator's oscillations

The figure below shows the results of our simulation by plotting the number of *X*, *Y*, and *Z* particles over time. As we can see, the system shows clear oscillatory behavior, with the concentrations of *X*, *Y*, and *Z* taking turns being at high concentration.

**STOP:** Why do you think that the repressilator motif leads to this pattern of oscillations?
{: .notice--primary}

![image-center](../assets/images/repress_graph.PNG){: .align-center}

* NOAH: please provide a caption with colors of particles indicated.

* NOAH: A natural question is what the period of this oscillation is and how this connects to real examples from the original repressilator paper.  Don't get in the weeds on this (max 10 minutes, but lmk what you think.)

Why would the repressilator's three-component feedback loop cause the concentrations of the three particles to oscillate? We will attempt to provide a high-level explanation.

Because the concentration of *X* starts out high, with no *Y* or *Z*, the concentration of *X* briefly increases because its rate of production exceeds its rate of degradation. Because there are no *Y* or *Z* particles present, they start increasing as well.

As soon as there are some *Z* particles present, the concentration of *X* peaks, and the reaction *Z* + *X* → *Z* occurs often enough for the rate of removal of *X* to exceed its rate of production, accounting for the first peak in the figure above.

Furthermore, because the concentration of *X* particles begins high, the reaction *X* + *Y* → *X* prevents the number of *Y* particles from growing quickly initially.

However, the remaining repression reaction (*Y* + *Z* → *Y*) has very little effect initially because the concentrations of *Y* and *Z* are both low. As a result, the rate of production of *Z* is higher than its rate of removal, and so its concentration increases.

In summary, after an initial rise, the concentration of *X* plummets, with the concentration of *Z* rising up to replace it, while the concentration of *Y* increases but at a slower rate than that of *Z*. This reflects the second peak in the figure above.

As a result, *Z* and *X* in effect have switched roles. Because there is a high concentration of *Z*, the reaction *Y* + *Z* → *Y* will suppress *Z* quickly, and it will decrease. Furthermore, because the concentration of *X* has decreased, the reaction *X* + *Y* → *X* will occur less often, allowing the concentration of *Y* to rise more quickly. Eventually, *Y* will be at high concentration while *Z* has reached a low concentration, accounting for the third peak in the figure above.

At this point, the reaction *X* + *Y* → *X* will suppress the concentration of *Y*. Because the concentration of *X* and *Z* are both lower, the reaction *Z* + *X* → *Z* will not greatly influence the concentration of *X*, which will rise to meet the following concentration of *Y*, and we have returned to our original situation, at which point the cycle will begin again.

## The power of noise

Take another look at the figure showing the oscillations of the repressilator. You will notice that the concentrations zigzag as they travel up or down, and that they peak at slightly different levels each time.

This noise in the repressilator's oscillations is due to variance as the particles travel around. Specifically, the repression reactions require two particles to collide in order for the reaction to take place. Due to random chance, these collisions may occur more or less often than they would be expected in a given time period because of random chance.

The noise that appears in the repressilator's oscillations is a feature, not a bug. As we have discussed previously, the cell's molecular interactions are inherently random. So if we see oscillations in a simulation that includes noise arising from random chance, we can be confident that this simulation is *robust* to a certain amount of noise.

In the next lesson, we will explore the concept of robustness further. The noise in the oscillations appears to be relatively minor, but what happens if our simulation experiences a much greater disturbance to the concentration of one of the particles?  Will it still be able to recover and return to the same oscillatory pattern?

[Next lesson](robust){: .btn .btn--primary .btn-large}
{: style="font-size: 100%; text-align: center;"}
