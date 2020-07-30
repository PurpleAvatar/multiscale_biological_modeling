---
permalink: /prologue/random-walk
title: "Random Walks"
sidebar:
 nav: "prologue"
---

## The wanderlust of a single randomly moving particle

In the previous two sections, we have discussed a central theme of our work in this course: the appearance of high-level behavior from simple rules.

Before we continue with seeing how this concept can be used to understand how zebras get their stripes, we will consider a simpler phenomenon by observing the movement of a single particle walking randomly in a two-dimensional plane. At each step, the particle moves a single unit in a randomly chosen direction. Before we show this animation, we ask a question.

**STOP**: After *n* steps, how far do you think the particle will have traveled (as the crow flies) from its starting point?

To answer this question, let's watch an animation of the particle and see for ourselves. If you're interested in building a simulation like this, sit tight --- we will soon see how to use the software used to generate this animation in the context of biological modeling.

<div style="text-align:center">
	<video width="640" height="480" controls>
	  <source type="video/mp4" src="../assets/random_walk_1.mp4">
	</video>
</div>

The distance that the particle wanders from its starting point may surprise you. And yet an astute scientist would point out that this is just a single particle; perhaps it has simply gone rogue, and a typical particle would be much more of a homebody.

Despite the fact that the particle's movements are random, there is a mathematical theorem that is able to predict the average-case behavior of the particle. This theorem states that after *n* steps of unit length in a random walk, a particle will on average find itself a distance of $\sqrt{n}$ from its origin.

## From one particle to many

This is not to say that after *n* steps our particle will be *exactly* distance $\sqrt{n}$ from the origin, any more than we would expect that after flipping a coin 2,000 times we would have seen  exactly 1,000 heads.  It is possible for the particle to have moved even farther out, or to wind up closer to the origin.

Yet the statement about the average behavior of a particle is powerful, and can be seen more clearly if we animate the action of many independent particles following random walks.

<div style="text-align:center">
	<video width="320" height="240" controls>
	  <source type="video/mp4" src="../assets/random_walk_200.mp4">
	</video>
</div>

Why should a scientist care about random walks? We will see later in this course that the model of the random walk, however simple, is nevertheless a powerful paradigm that bacteria like *E. coli* use to explore their environment in a search for food.

We also point out that our experience of the world confirms the statement that randomly walking particles will, on average, move farther and farther from their starting point. We understand, for example, that an infected COVID-19 patient can infect many others in an enclosed space in a short time frame. To take a less macabre example, we also know that when a cake is baking in the oven at home, we will not need to wait long for wonderful --- or terrible --- smells to waft outward from the kitchen.

## Big numbers in small spaces

Before we continue to the next lesson, we would point you to a beautiful animation illustrating just how far a single randomly moving particle can travel in a relatively small amount of time. This animation is part of the following excellent instructional video produced by the late Joel Stiles simulating the path taken by a glucose molecule as the result of Brownian motion.

{% include video id="KQgydF-fXvc&start=370" provider="youtube" %}

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/KQgydF-fXvc&start=370" frameborder="0" allowfullscreen></iframe>

Embed this video: https://www.youtube.com/watch?v=KQgydF-fXvc#t=6m10s

[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](animals){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

NOTE: PROVIDE detour of sorts proving sqrt(n) theorem.
