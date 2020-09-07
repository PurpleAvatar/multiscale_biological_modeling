---
permalink: /chemotaxis/home_conclusion
title: "Conclusion: The Beauty of *E. coli*'s Randomized Exploration Algorithm"
sidebar:
 nav: "chemotaxis"
toc: true
toc_sticky: true
---

## Two randomized exploration strategies

In this final lesson, we will use what we have learned about chemotaxis and the results of our BioNetGen model to build a random walk simulation emulating the behavior of *E. coli* within a background containing a variable concentration of attractant. We will then compare this model against a simple random walk model comparable to the one we introduced in the prologue in which the bacterium has a fixed tumbling frequency regardless of the concentration of attractant. Which "algorithm" will allow the bacterium to locate the attractant more readily?

In this simulation, a bacterium is represented by a point in two-dimensional space. At any point (*x*, *y*) in the space, there is some concentration *L*(*x*, *y*) of ligand; furthermore, we simulate an attractant gradient by ensuring that there is a point (called the **goal**) at which *L*(*x*, *y*) is maximized, with the concentration of attractant diminishing as the distance from this point increases.

Units in this space are in µm, so that moving from (0, 0) to (0, 20) is 20µm, a distance that we know from the introduction can be covered by the bacterium in 1 second during a contiguous run. The bacterium will start at the **origin** (0, 0), which we will establish to have a ligand concentration of 100 molecules/µm<sup>3</sup>. The maximum concentration of 10<sup>8</sup> molecules/µm<sup>3</sup> is located at the goal, requiring the bacterium to travel a fair distance to locate the attractant. The concentration of ligands [*L*] grows exponentially from the origin to the goal, so that that *L*(*x*, *y*) = 100 · 10<sup>8 · (1-*d*/*D*)</sup>, where *d* is the distance from (*x*, *y*) to the goal, and *D* is the distance from the origin to the goal.

**STOP:** How can we quantify how well a single bacterium has done at finding the attractant?
{: .notice--primary}

We will then implement two bacterial random walk strategies. In the first strategy, the bacterium travels in a new direction after an approximately constant rate of time. In the second strategy, the bacterium senses the relative concentration of attractant and adjusts its tumbling frequency, based on what we have learned about chemotaxis.

We will then run our random walk simulations many times for each strategy, where each simulation runs for some fixed time *t* in seconds. (This parameter should be large enough to allow the bacterium to have time to reach the goal.) For each simulated bacterium, we then measure how far it is from the goal. To compare the two strategies, we will compare the average distance to the goal for the simple random walk against the average distance to the goal for the realistic random walk.

Also keep in mind that if two mechanisms can get to the "food source" equally well, we will definitely want to get there faster. We will also consider this in comparing our performances.

**Strategy 1: Standard random walk**

Ingredients and simplifying assumptions of the model:
 - Run. The duration of run follows an exponential distrubtion with mean equals to the background run duration *t*<sub>0</sub>.
 - Tumble. The duration of cell tumble follows an exponential distribution with mean 0.1s[^Saragosti2012]. When it tumbles, we assume it only changes the orientation for the next run but doesn't move in space. The degree of reorientation follows a normal distribution with mean of 68° and standard deviation of 36°[^Berg1972].

For each cell, our simulation follows this procedure:

while *time* < duration:
- Sample the current run duration *curr_run_time*
- Run for *curr_run_time* second along current direction
- Sample the duration of tumble *curr_tumble_time* and the resulted direction
- increment t by *curr_run_time* and *curr_tumble_time*

[Visit standard random walk tutorial](tutorial_purerandom){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


**Strategy 2: Chemotactic random walk**

Ingredients and simplifying assumptions of the model:
 - Run. When no change in ligand concentration is detected, the duration of run follows an exponential distrubtion with mean equals to the background run duration *t*<sub>0</sub>. When the cell senses concentration change, the cell changes the expected run duration *t*, with *t* = *t*<sub>0</sub> * (1 + 10 · Δ[*L*]). Since expected run duration should always be positive, we require *t* = max(*t*, 0.000001). To account for the fact that tumbling can't be limitlessly reduced, we require *t* = min(*t*, 4 · *t*<sub>0</sub>).
 - Tumble. The duration of cell tumble follows an exponential distribution with mean 0.1s[^Saragosti2012]. When it tumbles, we assume it only changes the orientation for the next run but doesn't move in space. The degree of reorientation follows a normal distribution with mean of 68° and standard deviation of 36°[^Berg1972].
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

![image-center](../assets/images/chemotaxis_traj_compare.png){: .align-center}
<figcaption>Sample trajectories for the two strategies. Left: standard random walk; right: chemotactic random walk. The background color indicates concentration: white -> red = low -> high; black dots are starting points; red dots are the points they reached at the end of the simulation; colorful dashed lines represent trajectories (one color one cell): dark -> bright color = older -> newer time points; blue cross indicates the highest concentration (1500, 1500).</figcaption>

After 500 seconds, cells using the standard standard walk strategy travel away from the origin, and some of them are located at places with higher concentrations. The cells using chemotactic strategy, on the other hand, successfully move towards the goal and stay near it.

Let's compare the performance of 500 cells for 1500 seconds.

![image-center](../assets/images/chemotaxis_performance_compare.png){: .align-center}
<figcaption>Average distances through time. Left: standard random walk; right: chemotactic random walk The two colored lines indicate the two strategies, plotting average distances for the 500 cells; the shaded area is standard deviation; grey dashed line is where concentration reaches 1e8.</figcaption>

With standard random walk, the average distances towards the goal doesn't decrease. The large standard deviation indicates that many cells are closer to the goal, but many move in the wrong direction. With chemotactic strategy, the cells are able to get closer to the goal. The small standard deviation after the line flattens indicates that the cells are also able to stay near the goal.

Why is the chemotactic strategy better? It is almost as if the attractant detection serves as a "rubber band" -- if it's far from the bacterium, it is not allowed to go very far from the attractant.  As it nears it the tumbling frequency decreases which helps it travel farther. Once it hits the attractant anywhere that it goes, the tumbling frequency *increases*, preventing it from running far away.

## Why is bacterial background tumbling frequency constant across species?

The question we left unanswered is why that one tumble per second appears to be an evolutionarily stable strategy.

We will tweak the default tumbling frequency (represented as expected duration of run before each tumble, `time_exp`) for each simulation and see if some tumbling frequencies are better than others for bacteria to find the food.

Let's go back to the [chemotactic walk tutorial](tutorial_walk), and visualize the trajectories, and quantitatively compare the performances for different background tumbling frequencies.

With the visualization of trajectories, we see that the cells all move away from the starting point towards the target. However, how efficiently they get to the target is different for different expected run time. For example, after 500 seconds, the cells with `time_exp = 0.1` and `time_exp = 0.25` are still very far from the target; while those with `time_exp = 10` reach the target but don't stay there.

![image-center](../assets/images/chemotaxis_trajectories.png){: .align-center}
<figcaption>Sample trajectories for each tumbling frequency. The background color indicates concentration: white -> red = low -> high; black dots are starting points; red dots are the points they reached at the end of the simulation; colorful dashed lines represent trajectories (one color one cell): dark -> bright color = older -> newer time points.</figcaption>

What should a good trajectory look like? A cell should move fast towards the target; after reaching the goal, it should tumble immediately when moving to somewhere with a lower concentration and thus stay around the goal region. If we plot average distances to the goal through time, a good `time_exp` should be characterized by a fast decrease in distance to the goal, followed by flattening as close to the target as possible.

![image-center](../assets/images/chemotaxis_performance.png){: .align-center}
<figcaption>Average distances through time. Each colored line indicates a `time_exp`, plotting average distances for the 500 cells; the shaded area is standard deviation; grey dashed line is where concentration reaches 1e8.</figcaption>

There is a tradeoff between moving towards the target fast and staying there. For large `time_exp` values (10.0, 5.0, 2.0), distances to center decrease very quickly at the beginning of the simulation, but the cells don't stay there perfectly; the larger the `time_exp`, the further the distance becomes. For small `time_exp` values (0.1, 0.25, 0.5), the cells fail to move to the ligand efficiently. Note that for `time_exp = 0.5` and `time_exp = 1.0`, although both stay around the radius of saturation, `time_exp = 0.5` takes about 400s more. If you tried to allow 0.1 and 0.25 to flatten, they will take even longer.

Now we can answer the question of why 1 tumble per second. The goal of chemotaxis is to find the high concentration region and stay there; and the faster the cell can achieve this goal the better. If cells tumble too much, the goal can be achieved, but not efficiently; if tumble too little, they run by the attractant because they don't stop to sniff for food often enough.

Recall the video of *E. coli* moving towards to the sugar crystal.
<iframe width="640" height="360" src="https://www.youtube.com/embed/F6QMU3KD7zw" frameborder="0" allowfullscreen></iframe>

Our simulated *E. coli* do behave like those in the video. They generally move towards the crystal and stay close to it. Some run by the crystal, but then turn around to move toward the crystal again.

## Bacteria are even smarter than we thought

However, like most things in biology, the reality turns out to be even more complex than we might imagine.

One aspect of chemotaxis that is more advanced than we thought is the degree of reorientation. Consider - if a bacterium tumbles while moving up the gradient vs. moving down the gradient, how would the adjustment of degree of reorientation enable the cell to find food better?

The cell should turn a smaller angle if moving up a gradient - because moving to a very different direction might cause it to lose the gradient. And it should turn a larger angle if moving down the gradient, because turning around could be a good idea. This directional persistence when traveling up or down the gradient is observed in experiments.[^Saragosti2011]

With more experimental evidences, the model of *E. coli* chemotaxis has been constantly improved. That means the cellular systems powering bacteria like *E. coli* are even smarter than we originally thought!

## Exercises

1. Based on what we've learned about chemotaxis towards higher attractant concentrations, at a molecular level, how will the cell respond to a repellent gradient?
2. Modify the BNG model for [ligand receptor dynamics tutorial](tutorial_lr) to simulate one of the ligand-receptor system examples on [calculating steady state](home_signal). Does your simulation result match your calculation result?
3. Modify the BNG model provided in [tutorial on moving up gradient](tutorial_gradient) to simulate with `k_add = 0.1` and initial concentrations `L0 = 1e3` and `L0 = 1e5`. Compare to what we've simulated (`L0 = 1e4`), what differences do you observe?
4. As we discussed in the [adaptation section](tutorial_home_senseadap), there are different types of MCPs specific for different types of ligands. All the simulation we've built so far only used one type of ligand molecule. How will you change our BNG model to simulate the cell responds to two types of attractant molecules?
5. For the cellular level simulation provided in [tutorial on chemotactic random walk](tutorial_walk), how would you build gradients of two types of attractants with the highest concentration at different spots? What do you expect the trajectories look like? Run some simulations to confirm. (hint: modify the global parameters and modify the `calc_concentration` function).
6. For the cellular level simulation provided in [tutorial on chemotactic random walk](tutorial_walk), what will happen if the degree of reorientation when tumbling follows a uniform random distribution from 0° to 360°? Run some simulations to explore. (hint: modify the `tumble_move` function).



[^Saragosti2011]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2011. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[^Saragosti2012]: Saragosti J., Siberzan P., Buguin A. 2012. Modeling *E. coli* tumbles by rotational diffusion. Implications for chemotaxis. PLoS One 7(4):e35412. [available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3329434/).

[^Berg1972]: Berg HC, Brown DA. 1972. Chemotaxis in Escherichia coli analysed by three-dimensional tracking. Nature. [Available online](https://www.nature.com/articles/239500a0)

[^Baker2005]: Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)


[Next module](../coronavirus/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
