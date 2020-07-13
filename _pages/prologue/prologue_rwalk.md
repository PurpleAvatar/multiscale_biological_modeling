---
permalink: /prologue/rwalk
title: "Random Walks"
sidebar: 
 nav: "prologue"
---

* Let us take a step backward to consider a simple problem, which is observing the movement of a single particle walking randomly in a two-dimensional plane.
* We will see later that such a model, though simple, is the basis for how bacteria like E. coli explore their environment looking for food.
* But for now, let’s examine the path of the particle, which at each step is allowed to move a single unit in a random direction.
* We now ask a question: after n time steps, how far has the particle traveled from its starting point (as the crow flies)?
* To answer our question, et’s watch an animation of our single particle and see for ourselves. We will soon use the software used for building this animation in the context of biological modeling.

<div style="text-align:center">
	<video width="320" height="240" controls>
	  <source type="video/mp4" src="../assets/random_walk_1.mp4">
	</video>
</div>

* You may be surprised at how far the particle has wandered from its starting point. But this is just a single particle; perhaps its behavior is extremely nonstandard.  Perhaps the typical particle is much more of a homebody and continually returns to the origin.
* It turns out that despite the fact that the particle’s movements are random, there is a mathematical theorem that provides a surprising amount of understanding over its movement.  Specifically, after n steps of unit length, the particle is, on average, a distance of sqrt(n) away from the origin.
* This is not to say that the distance will be exactly sqrt(n) from the origin, any more than if we were to claim that flipping a coin 2,000 times would produce exactly 1,000 heads.  It is possible for the particle to move even farther out, or to wind up closer to the origin. But the typical particle will be about sqrt(n) away, as we can see when we animate the action of many particles following random walks independently.

<div style="text-align:center">
	<video width="320" height="240" controls>
	  <source type="video/mp4" src="../assets/random_walk_200.mp4">
	</video>
</div>

* Why should a scientist care? Because the fact that randomly particles will find themselves moving farther and farther away from their starting point explains much of what we already know about the world. Whether our particles are the viral particles in a superspreading event or the wonderful smells that drift upward from the kitchen in a multi-story house, we appreciate that randomly moving particles will spread out with absolute certainty.
* A beautiful animation illustrating just how far a single particle can travel in a relatively small amount of time is shown in the following excellent instructional video from the Pittsburgh Supercomputing Center simulating the path taken by a glucose molecule as the result of Brownian motion.

{% include video id="KQgydF-fXvc&start=370" provider="youtube" %}

Embed this video: https://www.youtube.com/watch?v=KQgydF-fXvc#t=6m10s


[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](animals){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
