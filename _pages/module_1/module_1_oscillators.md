---
permalink: /module_1/oscillators
title: "Oscillators"
sidebar: 
 nav: "mod1"
toc: true
toc_sticky: true
---


### Rules for Dampened Oscillations 

See “Setting-up Simulations” before starting these steps

Quick Tutorial: 
Load the file from Non-NAR tutorial
Change the Y molecule to have a diffusion constant of 2e-6
Add the following molecules
X, diffusion constant of 2e-6
Add the following reactions
Hidden' > Hidden' + X', rate: 4e2
X' > X' + Y' , rate: 5e2
Y' + X' > Y' , rate: 2e2
X' > NULL, rate: 1e3
Y' > NULL, rate: 3e2



