---
permalink: /motifs/tutorial_feed
title: "Feed-Forward Loop"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

* NOAH: Please flesh out this tutorial.

## Rules for Feedforward Loop

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

[Previous](tutorial_nar){: .btn .btn--primary .btn--x-large} [Next Page](tutorial_oscillators){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
