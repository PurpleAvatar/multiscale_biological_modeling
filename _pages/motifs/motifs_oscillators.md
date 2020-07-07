---
permalink: /motifs/oscillators
title: "Oscillators"
sidebar: 
 nav: "motifs"
toc: true
toc_sticky: true
---

*Now that we've seen...NAR & FFL... let's look at (motivation for oscillations)*

### The Repressilator

*Here's an explanation and motivation for the repressilator model. If you're more interested, see the expanded section under "Extras"*

### CellBlender Rules

If you are starting from the *file-name* file from *page-link*, you can use the following rules to view the oscillator.  

Change the Y molecule to have a diffusion constant of 2e-6
Add the following molecules
X, diffusion constant of 2e-6
Add the following reactions
Hidden' > Hidden' + X', rate: 4e2
X' > X' + Y' , rate: 5e2
Y' + X' > Y' , rate: 2e2
X' > NULL, rate: 1e3
Y' > NULL, rate: 3e2

### Full Tutorial

Starting from scratch

[Previous](feed){: .btn .btn--primary .btn--x-large} [Next Page](#){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


