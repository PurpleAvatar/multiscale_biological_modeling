---
permalink: /motifs/feed
title: "Feed-Forward Loop"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

* The previous section works if we have a transcription factor, but a normal gene is not a transcription factor and therefore is not able to negatively autoregulate.

* The question is how we can mimic the feedback process that we saw in the previous section to facilitate a speedup over simple regulation of *X* by *Y* in the case that *Y* is not a transcription factor.

### Rules for Feedforward Loop

See “Setting-up Simulations” before starting these steps

Quick Tutorial:
Load the file from Non-NAR tutorial
Change the Y molecule to have a diffusion constant of 2e-6
Add the following molecules
Change Y to a diffusion constant of 2e-6
X, diffusion constant of 2e-6
Z, diffusion constant of 2e-6
Add the following reactions
Hidden' -> Hidden' + X', rate: 4e2
X' -> X' + Y', rate: 5e2
X' -> X' + Z', rate: 1e3
Y' + Z' -> Y', rate: 3e4
X' -> NULL, rate: 1e3
Y' -> NULL, rate: 3e2
Z' -> NULL, rate: 5e2
Hidden’ -> NULL, 3e3

[Previous](nar){: .btn .btn--primary .btn--x-large} [Next Page](oscillators){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
