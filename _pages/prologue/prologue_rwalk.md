---
permalink: /prologue/random-walk
title: "Random Walks"
sidebar:
 nav: "prologue"
---

In the previous two sections, we have discussed a central theme of our work in this course: the appearance of high-level behavior from simple rules.

Before we continue with seeing how this concept can be used to understand how zebras get their stripes, we will consider a simpler phenomenon by observing the movement of a single particle walking randomly in a two-dimensional plane.  We will see later that this model, however simple, is a powerful implement that bacteria like *E. coli* use to explore their environment in a search for food.

But for now, let's examine the path of our particle, which makes a number of steps. At each step, the particle moves a single unit in a randomly chosen direction. Before we show this animation, we ask a question.

**STOP**: After *n* steps, how far do you think the particle will have traveled (as the crow flies) from its starting point?

To answer this question, let's watch an animation of the particle and see for ourselves. If you're interested in building a simulation like this, sit tight --- we will soon see how to use the software used to generate this animation in the context of biological modeling.

<div style="text-align:center">
	<video width="640" height="480" controls>
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

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/KQgydF-fXvc&start=370" frameborder="0" allowfullscreen></iframe>

Embed this video: https://www.youtube.com/watch?v=KQgydF-fXvc#t=6m10s


[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](animals){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
