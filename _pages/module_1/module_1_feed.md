---
permalink: /module_1/feed
title: "Feed-Forward Loop"
sidebar: 
 nav: "mod1"
toc: true
toc_sticky: true
---

*So we saw how the motif of NAR is useful. Motivations for FeedForward Loop. What if we want even faster?* 

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

