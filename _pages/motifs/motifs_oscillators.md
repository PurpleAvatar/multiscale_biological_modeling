---
permalink: /motifs/oscillators
title: "Building a Biological Oscillator"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

## Oscillators are everywhere in nature

* Humans, when placed in a bunker, maintain a roughly 24-hour cycle of sleep and activity (CITE)

* But **circadian rhythms** like these are visible throughout living things, even in cyanobacteria (CITE)

* Furthermore, cyclic life processes are not confined to circadian rhythms. Your heart and respiratory systems follow a cyclical process without you even thinking about it, and of course the cell cycle offers another example on a smaller scale across all cells.

* The underlying principle that unites all of these cyclical processes is **oscillation**. As one quantity rises, another falls, and the process cycles naturally by itself without any additional external process influencing it.

* We know that there isn't an intelligence driving these cyclic processes, and in fact they must be built upon very simple components.

## The repressilator

* There are many examples of network motifs that facilitate oscillation, some of which are very complicated with many moving parts. We will focus on a simple three-component oscillator motif called a **repressilator** (CITE).

* We will see how to implement this oscillator using a particle simulator but we will also analyze its *robustness* in contrast to the *fine-tuned* system for developing Turing patterns considered in the [prologue](prologue).

* The structure of a repressilator is shown in the figure below. In this motif, all three proteins are transcription factors, and they form a cycle in which *X* represses *Y*, *Y* represses *Z*, and *Z* represses *X* (hence the name).

* INSERT FIGURE.

* Define "repress".

* The repressilator certainly includes feedback, but nothing about this motif would indicate *a priori* that it would lead to oscillation.

**STOP:** Try building a reaction-diffusion model for the repressilator, assuming that we start with an initial concentration of *X* and no *Y* or *Z* particles.
{: .notice--primary}

## Modeling a repressilator with a reaction-diffusion particle simulation

* Building a model for the repressilator.

* *X*, *Y*, and *Z* all diffuse at the same rate.

* Phillip will start here.

[Next lesson](robust){: .btn .btn--primary .btn-large}
{: style="font-size: 100%; text-align: center;"}
