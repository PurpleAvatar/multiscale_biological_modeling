---
permalink: /chemotaxis/home_conclusion
title: "Conclusion: The Beauty of *E. coli*'s Randomized Exploration Algorithm"
sidebar:
 nav: "chemotaxis"
toc: true
toc_sticky: true
---

## Two randomized exploration strategies

In this final lesson of the module, we will use what we have learned about chemotaxis to build a random walk model emulating the behavior of *E. coli* within a background containing a variable concentration of attractant. The bacterium will reorient itself randomly, but it will be able to change its tumbling frequency based on the current relative concentration of attractant at its location.

We will then compare this realistic model of bacterial movement against a baseline algorithm modeling a fixed-tumbling frequency random walk. That is, the bacterium walks for a fixed distance and then reorients itself randomly. Which exploration algorithm allows the bacterium to locate the source of the attractant more reliably? And is one algorithm faster than the other?

We will represent a bacterium as a point in two-dimensional space. At any point (*x*, *y*), there is some concentration *L*(*x*, *y*) of ligand; furthermore, we simulate an attractant gradient by ensuring that there is a point (called the **goal**) at which *L*(*x*, *y*) is maximized, with the concentration of attractant diminishing as the distance from this point increases.

Units in this space will be in µm, so that moving from (0, 0) to (0, 20) is 20µm, a distance that we know from the introduction can be covered by the bacterium in 1 second during an uninterrupted run. The bacterium will start at the **origin** (0, 0), which we will establish to have a ligand concentration of 100 molecules/µm<sup>3</sup>. The goal contains a maximum concentration of 10<sup>8</sup> molecules/µm<sup>3</sup> and is located at the point (1500, 1500), requiring the bacterium to travel a significant distance to locate the attractant. The concentration of ligands [*L*] grows exponentially from the origin to the goal; specifically, *L*(*x*, *y*) = 100 · 10<sup>8 · (1-*d*/*D*)</sup>, where *d* is the distance from (*x*, *y*) to the goal, and *D* is the distance from the origin to the goal.

**STOP:** How can we quantify how well a bacterium has done at finding the attractant?
{: .notice--primary}

To measure average-case behavior, we will run our random walk simulations many times for each of our two strategies, where each simulation lasts some fixed time *t*. (This parameter should be large enough to allow the bacterium to have enough time to reach the goal.) To compare the two strategies, we will then measure how far on average a bacterium with each strategy ends up from the goal.

We now will specify the details of the two strategies.

###Strategy 1: Standard random walk

The duration of each run follows an exponential distribution with mean equal to an experimentally verified tun length.

When the cell tumbles, we assume that it only changes its orientation and does not change position. The degree of reorientation follows a uniform distribution from 0° to 360°. The duration of each tumble follows an exponential distribution with mean 0.1s[^Saragosti2012].

For a specified amount of time, the model takes the following steps. First, we select a random direction of movement along with a duration of our tumble. We then select a random duration to run and let the bacterium run in that direction for the specified amount of time. We then increment the total time by the time required for tumbling and running.

In the following tutorial, we simulate strategy 1 and use a Jupyter notebook to visualize the results of the simulation.

[Visit standard random walk tutorial](tutorial_purerandom){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


###Strategy 2: Chemotactic random walk

When no change in ligand concentration is detected, the duration of run follows an exponential distrubtion with mean equals to the background run duration *t*<sub>0</sub>. When the cell senses concentration change, the cell changes the expected run duration *t*, with *t* = *t*<sub>0</sub> * (1 + 10 · Δ[*L*]). Since expected run duration should always be positive, we require *t* = max(*t*, 0.000001). To account for the fact that tumbling can't be limitlessly reduced, we require *t* = min(*t*, 4 · *t*<sub>0</sub>).
 - Tumble. The duration of cell tumble follows an exponential distribution with mean 0.1s[^Saragosti2012]. When it tumbles, we assume it only changes the orientation for the next run but doesn't move in space. The degree of reorientation follows a uniform distribution from 0° to 360°.
 - Response. As we've seen in the BNG model, the cell can respond to the gradient change within 0.5 seconds. In this model, we allow cells to re-measure the concentration after it runs for 0.5 seconds.

For each cell, our simulation follows this procedure:

while *time* < duration:
- Assess the current concentration
- Update the current expected run duration *t*, sample the current run duration *curr_run_time*
- If *curr_run_time* < 0.5s:
    1. run for *curr_run_time* second along current direction
    2. Sample the duration of tumble *curr_tumble_time* and the resulted direction
    3. increment t by *curr_run_time* and *curr_tumble_time*
- If *curr_run_time* > 0.5s:
    1. run for 0.5s along current direction
    2. increment *time* by 0.5s (and then the cell will re-assess the new concentration, and decide the duration of next run)

[Visit chemotactic walk tutorial](tutorial_walk){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Comparing the two strategies

Visualize trajectories of 3 cells using strategy 1 versus strategy 2.
![image-center](../assets/images/chemotaxis_traj_compare_uniform.png){: .align-center}
Sample trajectories for the two strategies. Left: standard random walk; right: chemotactic random walk. The background color indicates concentration: white -> red = low -> high; black dots are starting points; red dots are the points they reached at the end of the simulation; colorful dashed lines represent trajectories (one color one cell): dark -> bright color = older -> newer time points; blue cross indicates the highest concentration (1500, 1500).
{: style="font-size: medium;"}

After 500 seconds, cells using the standard standard walk strategy travel away from the origin, and some of them are located at places with higher concentrations. The cells using chemotactic strategy, on the other hand, successfully move towards the goal and stay near it.

To confirm what we observed in the trajectories is representative of the performance of the two strategies, let's compare the performance of 500 cells for 1500 seconds. The following figure summarizes the average distances of the 500 cells for both strategies.

![image-center](../assets/images/chemotaxis_performance_compare_uniform.png){: .align-center}
Average distances through time. Red: standard random walk; blue: chemotactic random walk. The two colored lines indicates average distances for the 500 cells; the shaded area represents one standard deviation.
{: style="font-size: medium;"}

With standard random walk, the average distances towards the goal doesn't decrease. The large standard deviation indicates that many cells are closer to the goal, but many move in the wrong direction. With chemotactic strategy, the cells are able to get closer to the goal. The small standard deviation after the line flattens indicates that the cells are also able to stay near the goal.

Why is the chemotactic strategy better? It is almost as if the attractant detection serves as a "rubber band" -- if it's far from the bacterium, it is not allowed to go very far from the attractant.  As it nears it the tumbling frequency decreases which helps it travel farther. Once it hits the attractant anywhere that it goes, the tumbling frequency *increases*, preventing it from running far away.

## Why is bacterial background tumbling frequency constant across species?

The question we left unanswered is why that one tumble per second appears to be an evolutionarily stable strategy.

We will tweak the default tumbling frequency (represented as expected duration of run before each tumble, `time_exp`) for each simulation and see if some tumbling frequencies are better than others for bacteria to find the food.

Let's go back to the [chemotactic walk tutorial](tutorial_walk), and visualize the trajectories, and quantitatively compare the performances for different background tumbling frequencies.

With the visualization of trajectories, we see that the cells all move away from the starting point towards the target. However, how efficiently they get to the target is different for different expected run time. For example, after 800 seconds, the cells tumble every 0.2 second are still very far from the target; while those tumble every 5 seconds reach the target but don't stay there.

![image-center](../assets/images/chemotaxis_traj_0.2_uniform.png){: .align-center}
Sample trajectories for tumble every 0.2 second. The background color indicates concentration: white -> red = low -> high; black dots are starting points; red dots are the points they reached at the end of the simulation; colorful dashed lines represent trajectories (one color one cell): dark -> bright color = older -> newer time points; blue cross is (1500, 1500).
{: style="font-size: medium;"}

![image-center](../assets/images/chemotaxis_traj_1.0_uniform.png){: .align-center}
Sample trajectories for tumble every 1.0 second.
{: style="font-size: medium;"}

![image-center](../assets/images/chemotaxis_traj_5.0_uniform.png){: .align-center}
Sample trajectories for tumble every 5.0 second.
{: style="font-size: medium;"}

What should a good trajectory look like? A cell should move fast towards the target; after reaching the goal, it should tumble immediately when moving to somewhere with a lower concentration and thus stay around the goal region. If we plot average distances to the goal through time, a good `time_exp` should be characterized by a fast decrease in distance to the goal, followed by flattening as close to the target as possible.

To identify the background tumbling frequencies that allow the cells to reach the target fast and stay close to it, let's plot average distances of 500 cells to (1500, 1500) for a variety of background tumbling frequencies.

![image-center](../assets/images/chemotaxis_performance_uniform.png){: .align-center}
Average distances through time. Each colored line indicates a background tumbling frequency, plotting average distances for the 500 cells; the shaded area represents one standard deviation.
{: style="font-size: medium;"}

There is a tradeoff between moving towards the target fast and staying there. For large `time_exp` values (10.0, 5.0, 2.0), distances to center decrease very quickly at the beginning of the simulation, but the cells don't stay there perfectly; the larger the `time_exp`, the further the distance becomes. For small `time_exp` values (0.1, 0.2, 0.5), the cells fail to move to the ligand efficiently. Note that for `time_exp = 0.5` and `time_exp = 1.0`, although both stay around the radius of saturation, `time_exp = 0.5` takes about 400s more. If you tried to allow 0.1 and 0.25 to flatten, they will take even longer.

Now we can answer the question of why 1 tumble per second. The goal of chemotaxis is to find the high concentration region and stay there; and the faster the cell can achieve this goal the better. If cells tumble too much, the goal can be achieved, but not efficiently; if tumble too little, they run by the attractant because they don't stop to sniff for food often enough.

Recall the video of *E. coli* moving towards to the sugar crystal.
<iframe width="640" height="360" src="https://www.youtube.com/embed/F6QMU3KD7zw" frameborder="0" allowfullscreen></iframe>

Our simulated *E. coli* do behave like those in the video. They generally move towards the crystal and stay close to it. Some run by the crystal, but then turn around to move toward the crystal again.

## Bacteria are even smarter than we thought

However, like most things in biology, the reality turns out to be even more complex than we might imagine.

One aspect of chemotaxis that is more advanced than we thought is the degree of reorientation. Instead of uniformly sample from 0° to 360°, the degree of reorientation when no attractant/repellant presents follows a normal distribution with mean of 68° and standard deviation of 36°[^Berg1972]. Moreover, the degree of reorientation depends on whether the cell is travelling along the correct direction. Consider - if a bacterium tumbles while moving up the gradient vs. moving down the gradient, how would the adjustment of degree of reorientation enable the cell to find food better? The cell should turn a smaller angle if moving up a gradient - because moving to a very different direction might cause it to lose the gradient. And it should turn a larger angle if moving down the gradient, because turning around could be a good idea. This directional persistence when traveling up or down the gradient is observed in experiments.[^Saragosti2011] We will explore the benefit of these in Exercise X.

With more experimental evidences, the model of *E. coli* chemotaxis has been constantly improved. That means the cellular systems powering bacteria like *E. coli* are even smarter than we originally thought!

[^Saragosti2011]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2011. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[^Saragosti2012]: Saragosti J., Siberzan P., Buguin A. 2012. Modeling *E. coli* tumbles by rotational diffusion. Implications for chemotaxis. PLoS One 7(4):e35412. [available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3329434/).

[^Berg1972]: Berg HC, Brown DA. 1972. Chemotaxis in Escherichia coli analysed by three-dimensional tracking. Nature. [Available online](https://www.nature.com/articles/239500a0)

[^Baker2005]: Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)


[Exercises](home_exercise){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
