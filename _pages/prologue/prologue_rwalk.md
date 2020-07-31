---
permalink: /prologue/random-walk
title: "An Introduction to Random Walks"
sidebar:
 nav: "prologue"
---

## The wanderlust of a single particle

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

Despite the fact that the particle's movements are random, there is a mathematical theorem that is able to predict the average-case behavior of the particle. This theorem states that after *n* steps of unit length in a random walk, a particle will on average find itself a distance of approximately $$\sqrt{n}$$ from its origin. (For the mathematically inclined, we explain why this is true in a bonus section at the bottom of this page.)

## From one particle to many

This is not to say that after *n* steps our particle will be *exactly* distance $$\sqrt{n}$$ from the origin, any more than we would expect that after flipping a coin 2,000 times we would have seen  exactly 1,000 heads.  It is possible for the particle to have moved even farther out, or to wind up closer to the origin.

Yet the statement about the average behavior of a particle is powerful, and can be seen more clearly if we animate the action of many independent particles following random walks.

<div style="text-align:center">
	<video width="640" height="480" controls>
	  <source type="video/mp4" src="../assets/random_walk_200.mp4">
	</video>
</div>

Why should a scientist care about random walks? We will see later in this course that the model of the random walk, however simple, is nevertheless a powerful paradigm that bacteria like *E. coli* use to explore their environment in a search for food.

We also point out that our experience of the world confirms the statement that randomly walking particles will, on average, move farther and farther from their starting point. We understand, for example, that an infected COVID-19 patient can infect many others in an enclosed space in a short time frame. To take a less macabre example, we also know that when a cake is baking in the oven at home, we will not need to wait long for wonderful --- or terrible --- smells to waft outward from the kitchen.

## Big numbers in small spaces

Before we continue to the next lesson, we would point you to a beautiful animation illustrating just how far a single randomly moving particle can travel in a relatively small amount of time. This animation is part of the following excellent instructional video produced by the late Joel Stiles. It begins at around the 6:10 mark, which shows a simulation of the path taken by a glucose molecule as the result of Brownian motion.

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/KQgydF-fXvc?start=370" frameborder="0" allowfullscreen></iframe>

[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](animals){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

## A proof of the expected distance theorem

Above, we stated that the average distance that a random particle would find itself from its starting point after taking *n* steps of unit length is $$\sqrt{n}$$. Below, we provide a justification for why this is true for interested learners who are familiar with probability.

Let $$\mathbf{x_i}$$ denote the random variable corresponding to the vector of the particle's *i*-th step.  The distance *d* traveled by the particle can be represented by the sum of all these vectors,

$$d = \mathbf{x_1} + \mathbf{x_2} + \cdots + \mathbf{x_n} \,.$$

We will show that the expected value of $$d^2$$ is equal to *n*. To do so, note that

$$d^2 = (\mathbf{x_1} + \mathbf{x_2} + \cdots + \mathbf{x_n}) \cdot (\mathbf{x_1} + \mathbf{x_2} + \cdots + \mathbf{x_n})\,.$$

After expanding the right side of this equation, we obtain

$$d^2 = \mathbf{x_1} \cdot (\mathbf{x_1} + \mathbf{x_2} + \cdots + \mathbf{x_n}) + \mathbf{x_2} \cdot (\mathbf{x_1} + \mathbf{x_2} + \cdots + \mathbf{x_n}) + \cdots + \mathbf{x_n}) \cdot (\mathbf{x_1} + \mathbf{x_2} + \cdots + \mathbf{x_n}) \,.$$

Finally, we rearrange this equation so that the terms $$\mathbf{x_1} \cdot \mathbf{x_1}$$, $$\mathbf{x_2} \cdot \mathbf{x_2}$$, and so on occur first, and the remaining terms appear last. We can therefore write $$d^2$$ as follows.

$$d^2 = \sum_{i=1}^n (\mathbf{x_i} \cdot \mathbf{x_i}) + \sum_{i \neq j} (\mathbf{x_i} \cdot \mathbf{x_j})\, .$$

The right side of this equation is the sum of $$n^2$$ dot products.  When we take the expectation of both sides, then we apply the fundamental result called the "linearity of expectation", which states that for any two random variables $$x$$ and $$y$$, the expectation of their sum $$\mathbb{E}(x + y)$$ is equal to the sum of the corresponding expectations $$\mathbb{E}(x) + \mathbb{E}(y)$$:

$$\mathbb{E}(d^2) = \sum_{i=1}^n E(\mathbf{x_i} \cdot \mathbf{x_i}) + \sum_{i \neq j} E(\mathbf{x_i} \cdot \mathbf{x_j})\, .$$

For any *i*, $$\mathbb{E}(\mathbf{x_i} \cdot \mathbf{x_i})$$ is just the length of the vector $$x_i$$, which is equal to 1.  On the other hand, the expected value of the dot product of any two random unit vectors is zero.  Therefore, the right side of the above equation can be simplified to give the equation

$$\mathbb{E}(d^2) = \sum_{i=1}^n (1) + \sum_{i \neq j} (0) = n + 0 = n\, ,$$

which is what we set out to show.

A couple of notes before we continue. First, we did not use anything about the random walk being two- dimensional in this proof; accordingly, it holds whether our particle is walking in two, three, or any number of dimensions.

Second, we technically did not show that the expected value of $$d$$ is $$\sqrt{n}$$, but rather that the expected value of $$d^2$$ is $$n$$. It is not exactly true that $$\mathbb{E}(d)$$ is equal to $$\sqrt{n}$$, but rather that as $$n$$ grows, $$\mathbb{E}(d)$$ grows like a constant factor of $$n$$. It is beyond the scope of this course, but it can be shown that as $$n$$ goes off to infinity, $$\mathbb{E}(d)$$ tends toward $$\sqrt{\dfrac{2}{\pi} \cdot n}$$. Who knew that random walks could get so complicated!
