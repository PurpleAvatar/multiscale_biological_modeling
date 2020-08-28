---
permalink: /chemotaxis/home_conclusion
title: "Conclusion"
sidebar:
 nav: "chemotaxis"
---

## Background tumbling frequency

In this module, we have built a model that replicates the chemotaxis pathway in *E. coli*, and we have seen how *E. coli* can adjust the tumbling frequency in response to ligand concentration changes. What we have not answered is *why* it is a good strategy for *E. coli* to tumble less frequently in the presence of increasing attractant. Put more simply, does decreasing this tumbling frequency allow the bacterium to find food more quickly?

To address this question, we will use what we have learned about chemotaxis and our BNG model results to build a random walk simulation emulating the behavior of *E. coli*. We will then compare this model against a simple random walk model comparable to the one we introduced in the prologue in which the bacterium has a fixed tumbling frequency regardless of the concentration of attractant. Which "algorithm" will allow the bacterium to locate the attractant more readily?

In this simulation, a bacterium is represented by a point in two-dimensional space. At any point (*x*, *y*) in the space, there is some concentration *L*(*x*, *y*) of ligand; furthermore, we simulate an attractant by ensuring that there is a point (called the **goal**) at which *L*(*x*, *y*) is maximized, with the concentration of attractant diminishing as the distance from this point increases.

Units in this space are in µm, so that moving from (0, 0) to (0, 20) is 20µm, a distance that we know from the introduction can be covered by the bacterium in 1 second if it does not stop to tumble. The bacterium will start at (0, 0), which we will establish to have a ligand concentration of 100 molecules/µm<sup>3</sup>. The maximum concentration of 1e8.5 molecules/µm<sup>3</sup> is located at the goal (1200, 1200), requiring the bacterium to travel a fair distance to locate the attractant.

* SHUANGER: Why 1e8.5?  Why not an integer exponent?  Or just saying, for example, 10 million?  And why 1200?  This too is a weird number that would make it seem like we are trying to force the model.

* SHUANGER: need a rewritten paragraph here explaining what an exponential gradient is, and how we can compute it based on the distance from 1200, 1200.

**STOP:** How can we quantify how well a single bacterium has done at finding the attractant?
{: .notice--primary}

We will then implement two bacterial strategies. The first strategy is a standard random walk in which the bacterium reorients itself after a fixed rate of time. The second is based on what we have learned about chemotaxis.

* SHUANGER: insert a *very precisely* defined model of how the bacterium responds to its environment based on concentration.

We will then run our random walk simulations many times for each strategy, where each simulation runs for some fixed time *t* in seconds. (This parameter should be large enough to allow the bacterium to have time to reach the goal.) For each simulated bacterium, we then measure how far it is from the goal. To compare the two strategies, we will compare the average distance to the goal for the simple random walk against the average distance to the goal for the realistic random walk.

Also keep in mind that if two mechanisms can get to the "food source" equally well, we will definitely want to get there faster.

* SHUANGER: this is a good point but does it appear in our simulations?

* SHUANGER: we should have a separate tutorial that focuses *only* on verifying that the random walk is indeed a good strategy.  Let's just use a tumbling frequency of 1 per second for now.  I'd like to verify that

## New section

* SHUANGER: Here is where we should have a comparison of the pure random walk against the empirical strategy.  We should then reflect on why the empirical strategy is better.  It is almost as if the attractant detection serves as a "rubber band" -- if it's far from the bacterium, it is not allowed to go very far from the attractant.  As it nears it the tumbling frequency decreases which helps it travel farther. Once it hits the attractant anywhere that it goes, the tumbling frequency *increases*, preventing it from running far away.  This may be where we insert the original chemotaxis video but let's see what you come up with first.

## New section

* SHUANGER: Now is where we get into the details of the fact that 1 tumble per second appears to be an evolutionarily stable strategy.

We will tweak the default tumbling frequency (represented as expected duration of run before each tumble, `time_exp`) for each simulation and see if some tumbling frequencies are better than others for bacteria to find the food.

[Visit random walk tutorial](tutorial_walk){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

With the visualization of trajectories, we see that the cells all move away from the starting point towards the target. However, how efficiently they get to the target is different for different expected run time. For example, after 500 seconds, the cells with `time_exp = 0.1` and `time_exp = 0.25` are still very far from the target; while those with `time_exp = 10` reach the target but don't stay there.

![image-center](../assets/images/chemotaxis_trajectories.png){: .align-center}
<figcaption>Sample trajectories for each tumbling frequency. The background color indicates concentration: white -> red = low -> high; black dots are starting points; red dots are the points they reached at the end of the simulation; colorful dashed lines represent trajectories (one color one cell): dark -> bright color = older -> newer time points; dark dashed circle is where concentration reaches 1e8.</figcaption>

What should a good trajectory look like? A cell should move fast towards the target; after reaching the target, it should tumble immediately when moving to somewhere with a lower concentration and thus stay around the target region. If we plot average distances to the target through time, a good `time_exp` should be characterized by a fast decrease in distance to the target, followed by flattening as close to the target as possible.

![image-center](../assets/images/chemotaxis_performance.png){: .align-center}
<figcaption>Average distances through time. Each colored line indicates a `time_exp`, plotting average distances for the 500 cells; the shaded area is standard deviation; grey dashed line is where concentration reaches 1e8.</figcaption>

There is a tradeoff between moving towards the target fast and staying there. For large `time_exp` values (10.0, 5.0, 2.0), distances to center decrease very quickly at the beginning of the simulation, but the cells don't stay perfectly around the radius of saturation; the larger the `time_exp`, the further the distance becomes. For small `time_exp` values (0.1, 0.25, 0.5), the cells fail to move to the ligand efficiently. Note that for `time_exp = 0.5` and `time_exp = 1.0`, although both stay around the radius of saturation, `time_exp = 0.5` takes about 200s more. If you tried to allow 0.1 and 0.25 to flatten, they will take even longer.

Later we should focus on: why there is a background tumbling frequency of one tumble every second?

Now we can answer the question of why 1 tumble per second. The goal of chemotaxis is to find the high concentration region and stay there; and the faster the cell can achieve this goal the better. If cells tumble too much, the goal can be achieved, but not efficiently; if tumble too little, they run by the attractant because they don't stop to sniff for food often enough.

Recall the video of *E. coli* moving towards to the sugar crystal.
<iframe width="640" height="360" src="https://www.youtube.com/embed/F6QMU3KD7zw" frameborder="0" allowfullscreen></iframe>

Our simulated *E. coli* do behave like those in the video. They generally move towards the crystal and stay close to it. Some run by the crystal, but then turn around to move toward the crystal again.

## Smarter than we thought

However, like most things in biology, the reality turns out to be even more complex than we might imagine.

One aspect of chemotaxis that is more advanced than we thought is the degree of reorientation. Consider - if a bacterium tumbles while moving up the gradient vs. moving down the gradient, how would the adjustment of degree of reorientation enable the cell to find food better?

The cell should turn a smaller angle if moving up a gradient - because moving to a very different direction might cause it to lose the gradient. And it should turn a larger angle if moving down the gradient, because turning around could be a good idea. This directional persistence when traveling up or down the gradient is observed in experiments[^Saragosti2011].

With more experimental evidences, the model of *E. coli* chemotaxis has been constantly improved. That means the cellular systems powering bacteria like *E. coli* are even smarter than we originally thought!

## Exercise

1. Based on what we've learned about chemotaxis towards higher attractant concentrations, at a molecular level, how will the cell respond to a repellent gradient?
2. Modify the BNG model for [ligand receptor dynamics tutorial](tutorial_lr) to simulate one of the ligand-receptor system examples on [calculating steady state](home_signal). Does your simulation result match your calculation result?
3. Modify the BNG model provided in [tutorial on moving up gradient](tutorial_gradient) to simulate with `k_add = 0.1` and initial concentrations `L0 = 1e3` and `L0 = 1e5`. Compare to what we've simulated (`L0 = 1e4`), what differences do you observe?
4. As we discussed in the [adaptation section](tutorial_home_senseadap), there are different types of MCPs specific for different types of ligands. All the simulation we've built so far only used one type of ligand molecule. How will you change our BNG model to simulate the cell responds to two types of attractant molecules?
5. For the cellular level simulation provided in [tutorial on chemotactic random walk](tutorial_walk), how would you build gradients of two types of attractants with the highest concentration at different spots? What do you expect the trajectories look like? Run some simulations to confirm. (hint: modify the global parameters and modify the `calc_concentration` function).
6. For the cellular level simulation provided in [tutorial on chemotactic random walk](tutorial_walk), what will happen if the degree of reorientation when tumbling follows a uniform random distribution from 0° to 360°? Run some simulations to explore. (hint: modify the `tumble_move` function).



[^Saragosti2011]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2011. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)


[Next chapter](../coronavirus/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
