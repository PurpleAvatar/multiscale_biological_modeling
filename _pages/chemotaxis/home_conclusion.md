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
 - Tumble. The duration of cell tumble follows an exponential distribution with mean 0.1s[^Saragosti2012]. When it tumbles, we assume it only changes the orientation for the next run but doesn't move in space. The degree of reorientation follows a uniform distribution from 0° to 360°.

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

![image-center](../assets/images/chemotaxis_traj_compare_uniform.png){: .align-center}
<figcaption>Sample trajectories for the two strategies. Left: standard random walk; right: chemotactic random walk. The background color indicates concentration: white -> red = low -> high; black dots are starting points; red dots are the points they reached at the end of the simulation; colorful dashed lines represent trajectories (one color one cell): dark -> bright color = older -> newer time points; blue cross indicates the highest concentration (1500, 1500).</figcaption>

After 500 seconds, cells using the standard standard walk strategy travel away from the origin, and some of them are located at places with higher concentrations. The cells using chemotactic strategy, on the other hand, successfully move towards the goal and stay near it.

To confirm what we observed in the trajectories is representative of the performance of the two strategies, let's compare the performance of 500 cells for 1500 seconds. The following figure summarizes the average distances of the 500 cells for both strategies.

![image-center](../assets/images/chemotaxis_performance_compare_uniform.png){: .align-center}
<figcaption>Average distances through time. Red: standard random walk; blue: chemotactic random walk. The two colored lines indicates average distances for the 500 cells; the shaded area represents one standard deviation.</figcaption>

With standard random walk, the average distances towards the goal doesn't decrease. The large standard deviation indicates that many cells are closer to the goal, but many move in the wrong direction. With chemotactic strategy, the cells are able to get closer to the goal. The small standard deviation after the line flattens indicates that the cells are also able to stay near the goal.

Why is the chemotactic strategy better? It is almost as if the attractant detection serves as a "rubber band" -- if it's far from the bacterium, it is not allowed to go very far from the attractant.  As it nears it the tumbling frequency decreases which helps it travel farther. Once it hits the attractant anywhere that it goes, the tumbling frequency *increases*, preventing it from running far away.

## Why is bacterial background tumbling frequency constant across species?

The question we left unanswered is why that one tumble per second appears to be an evolutionarily stable strategy.

We will tweak the default tumbling frequency (represented as expected duration of run before each tumble, `time_exp`) for each simulation and see if some tumbling frequencies are better than others for bacteria to find the food.

Let's go back to the [chemotactic walk tutorial](tutorial_walk), and visualize the trajectories, and quantitatively compare the performances for different background tumbling frequencies.

With the visualization of trajectories, we see that the cells all move away from the starting point towards the target. However, how efficiently they get to the target is different for different expected run time. For example, after 800 seconds, the cells tumble every 0.2 second are still very far from the target; while those tumble every 5 seconds reach the target but don't stay there.

![image-center](../assets/images/chemotaxis_traj_0.2_uniform.png){: .align-center}
<figcaption>Sample trajectories for tumble every 0.2 second. The background color indicates concentration: white -> red = low -> high; black dots are starting points; red dots are the points they reached at the end of the simulation; colorful dashed lines represent trajectories (one color one cell): dark -> bright color = older -> newer time points; blue cross is (1500, 1500).</figcaption>

![image-center](../assets/images/chemotaxis_traj_1.0_uniform.png){: .align-center}
<figcaption>Sample trajectories for tumble every 1.0 second.</figcaption>
 
![image-center](../assets/images/chemotaxis_traj_5.0_uniform.png){: .align-center}
<figcaption>Sample trajectories for tumble every 5.0 second.</figcaption>

What should a good trajectory look like? A cell should move fast towards the target; after reaching the goal, it should tumble immediately when moving to somewhere with a lower concentration and thus stay around the goal region. If we plot average distances to the goal through time, a good `time_exp` should be characterized by a fast decrease in distance to the goal, followed by flattening as close to the target as possible.

To identify the background tumbling frequencies that allow the cells to reach the target fast and stay close to it, let's plot average distances of 500 cells to (1500, 1500) for a variety of background tumbling frequencies.

![image-center](../assets/images/chemotaxis_performance_uniform.png){: .align-center}
<figcaption>Average distances through time. Each colored line indicates a background tumbling frequency, plotting average distances for the 500 cells; the shaded area represents one standard deviation.</figcaption>

There is a tradeoff between moving towards the target fast and staying there. For large `time_exp` values (10.0, 5.0, 2.0), distances to center decrease very quickly at the beginning of the simulation, but the cells don't stay there perfectly; the larger the `time_exp`, the further the distance becomes. For small `time_exp` values (0.1, 0.2, 0.5), the cells fail to move to the ligand efficiently. Note that for `time_exp = 0.5` and `time_exp = 1.0`, although both stay around the radius of saturation, `time_exp = 0.5` takes about 400s more. If you tried to allow 0.1 and 0.25 to flatten, they will take even longer.

Now we can answer the question of why 1 tumble per second. The goal of chemotaxis is to find the high concentration region and stay there; and the faster the cell can achieve this goal the better. If cells tumble too much, the goal can be achieved, but not efficiently; if tumble too little, they run by the attractant because they don't stop to sniff for food often enough.

Recall the video of *E. coli* moving towards to the sugar crystal.
<iframe width="640" height="360" src="https://www.youtube.com/embed/F6QMU3KD7zw" frameborder="0" allowfullscreen></iframe>

Our simulated *E. coli* do behave like those in the video. They generally move towards the crystal and stay close to it. Some run by the crystal, but then turn around to move toward the crystal again.

## Bacteria are even smarter than we thought

However, like most things in biology, the reality turns out to be even more complex than we might imagine.

One aspect of chemotaxis that is more advanced than we thought is the degree of reorientation. Instead of uniformly sample from 0° to 360°, the degree of reorientation when no attractant/repellant presents follows a normal distribution with mean of 68° and standard deviation of 36°[^Berg1972]. Moreover, the degree of reorientation depends on whether the cell is travelling along the correct direction. Consider - if a bacterium tumbles while moving up the gradient vs. moving down the gradient, how would the adjustment of degree of reorientation enable the cell to find food better? The cell should turn a smaller angle if moving up a gradient - because moving to a very different direction might cause it to lose the gradient. And it should turn a larger angle if moving down the gradient, because turning around could be a good idea. This directional persistence when traveling up or down the gradient is observed in experiments.[^Saragosti2011] We will explore the benefit of these in Exercise X.

With more experimental evidences, the model of *E. coli* chemotaxis has been constantly improved. That means the cellular systems powering bacteria like *E. coli* are even smarter than we originally thought!

## Exercises

**1.How do *E. coli* respond to repellants?**

1. Based on what we've learned about chemotaxis towards higher attractant concentrations, can you summarize how would *E. coli* cells repond to an repellant?

2. In [phosphorylation tutorial](tutorial_phos), we defined the rate constant for free CheA autophosphorylation `k_T_phos`, and specified that when the receptor complex is bound to an attractant molecule, the autophosphorylation rate constant becomes `0.2 · k_T_phos`. Now, let's further specify that when the receptor complex is bound to a **repellant** molecule, the autophosphorylation rate constant becomes `5 · k_T_phos`. Please implement this rule in our BNG model.

3. If our system does not have attractant molecules, but instead, was added with `L0` repellant molecules at the beginning of the simulation. Please simulate the system with `L0 = 5000` and `L0 = 1e5` and observe the concentrations of chemical species for 3 seconds. How does the concentration of phosphorylated CheY change? What does that implicate?

**2.What if there are multiple attractant sources?**

1. So far our model only included one type of attractant and one type of receptor. However, *E. coli* has different receptors specific for different types of attractants. Assuming all receptor types influence the downstream reactions equally, can we include multiple ligand/receptor types into our model easily? Please modify your model from [adaptation tutorial](tutorial_senseadap) to reflect 2 types of receptor specific for 2 types of ligand (call them *A* and *B*). Assume we have 3500 receptor molecules of each type. (*Hint*: you won't need to have additional chemical species for `L` and `T`; just specify additional states for them, for example `L(t,Lig~A)` only binds with `T(l,Lig~A)`. Don't forget to update `seed species`.)

2. What will happen if after the cell adapts to concentration of one type of attractant, another type of attractant is suddenly added to the system? Let's model a scenerio such that after the cell adapts to `1e6` ligand molecules *A*, suddenly add `1e6` ligand molecules *B*. To achieve this, we can specify the rate constant for binding of B and its receptor with a `function`: if the cell hasn't adapt to [*A*], the rate constant is 0; otherwise the rate is `k_lr_bind` (Recall defining `function`s in [up-gradient tutorial](tutorial_gradient)). Please observe the concentrations of phosphorylated CheY. Is the cell able to respond to ligand *B* after adapting to the concentration of ligand *A*? (*Hint*: you can judge whether the cell is adapted to `1e6` ligand *A* molecules by methylation levels.)

3. What if there are two nutrient rich locations? In [chemotactic walk tutorial](tutorial_walk), we have a concentration gradient growing exponential from center to the goal (1500, 1500), so that *L(x,y)* = 100 · 10<sup>8 · (1-*d*/*D*)</sup>. Please modify your model from the tutorial to include another goal at location (-1500, 1500), and a similar concentration gradient growing from the center to the goal. The new concentration of ligands, [*L*] will be *L(x,y)* = 100 · 10<sup>8 · (1-*d*<sub>1</sub>/*D*<sub>1</sub>)</sup> + 100 · 10<sup>8 · (1-*d*<sub>2</sub>/*D*<sub>2</sub>)</sup>, where *d*<sub>1</sub> is the distance from *(x,y)* to goal1 (1500, 1500), *d*<sub>2</sub> is the distance from *(x,y)* to goal2 (-1500, 1500), and *D*<sub>1</sub> = *D*<sub>2</sub> are the distances from the origin to goal1 and goal2. Please simulate with tumble every 1 second as the background tumbling frequency, and visualize trajectories for several cells. Are the cells able to find the goals?

**3.The actual tumbling reorientation is smarter than our model?**

Earlier we said that when *E. coli* tumbles, the degree of reorientation is actually not uniformly random from 0° to 360°. With background ligand concentration, the degree of reorientation approximately follows a normal distribution with mean of 68° and standard deviation of 36°. Recent research suggests that when the cell is moving up the gradient, the degree of reorientation is smaller (although we don't have definitive measurements for now)[^Saragosti2011]. Please modify your model from [chemotactic walk tutorial](tutorial_walk) to change the random uniform sampling to the "smarter" sampling. Specifically, in the `tumble_move(curr_dir)` function, replace `new_dir = np.random.uniform(low = 0.0, high = 2 * math.pi)` with
~~~ python
if up_gradient:
		new_dir = np.random.normal(loc = tumble_angle_mu - 0.1, scale = tumble_angle_std)
else:
	new_dir = np.random.normal(loc = tumble_angle_mu, scale = tumble_angle_std)
new_dir *= np.random.choice([-1, 1])
~~~
and set `tumble_angle_mu = 2 * math.pi * 68 / 360`, and `tumble_angle_std = 2 * math.pi * 36 / 360` as global parameters. Please implement `up_gradient` as an argument for the updated `tumble_move` function. (*Hint*: `up_gradient` can be decided based on `curr_conc` and `past_conc` during the simulation). Please quantitatively measure the chemotaxis performance by calculating the mean and standard deviation of each cell's distance to the goal for 500 cells (you can do that for different background tumbling frequencies too). Why are the cells able to find the goal faster?

**4. Want another BNG model?**

Like what we've seen in this module, BNGL is very good at simulating systems that involve a large number of species and particles yet can be summarized with a small set of rules. Polymerization reactions is another good example of such systems. **Polymerization** is the process of monomer molecules react to form polymer chains, for example, polyvinyl chloride (PVC) is formed from many vinyl polymers. We can build a simplified BNGL model to simulate the polymerization of monomer *A* to form polymer *AAAAAA*... The reaction can be written as *A*<sub>m</sub> + *A*<sub>n</sub> -> *A*<sub>m+n</sub>. There are two sites on `A` that are involved in the reaction: one "head" to join a free "tail", and one "tail" to allow a "head" to bind. We will model a polymerization reaction with BNGL (this model is inspired by the [BLBR model in official BNG tutorials](https://github.com/RuleWorld/BNGTutorial/blob/master/CBNGL/BLBR.bngl)).

Please open a new `.bngl` file. We will have only one moleclue type: `A(h,t)`; the `s` and `t` indicates the "head" and "tail". Please implement the four reaction rules: 
- initializing the series of reactions: two unbound `A` forms the intial dimer; 
- adding an unbound `A` to the "tail" of an existing `A` n-mer to form an `A` (n+1)-mer; 
- adding an existing `A` n-mer to the "tail" of an unbound `A` to form an (n+1)-mer;
- adding an existing `A` m-mer to the "tail" of an existing `A` n-mer to form an (n+m)-mer.
 (*Hint*: check out the `!+` grammar in the [ultimate BNG guide](http://comet.lehman.cuny.edu/griffeth/BioNetGenTutorialFromBioNetWiki.pdf).) Set all reaction rate constants to be 1.

We will simulate with 1000 `A` monomers at the beginning of the simulation, and observe for the formation of polymers composed of different number of `A`s. To do so, we select the pattern of containing *x* `A`s with `A == x`. `Species` instead of `Molecules` is required for selecting polymer patterns.

	begin seed species
		A(h,t) 1000
	end seed species

	begin observables
		Species A1 A==1
		Species A2 A==2
		Species A3 A==3
		Species A4 A==4
		Species A5 A==5
		Species ALongChains A>10
	end observables

For this model, let's try another simulation method - **Network-free** simulation. It is similar to SSA simulation we used before, but instead of simulating transitions between states of the whole *system*, it tracks individual *particles*. In this polymerization model, the possible number of reactions are much higher - we can have any m-mer reacting with any n-mer at any step. Considering all these possible reactions makes SSA slow. Luckily, we don't have that many particles, so trucking each particle will be much faster (in our chemotaxis model, tracking over 10<sup>8</sup> molecules individually is difficult).

Please simulate with the command `simulate({method=>"nf", t_end=>100, n_steps=>100})`. Note that we do not need the `generate_network()` command. What do you observe?



[^Saragosti2011]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2011. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[^Saragosti2012]: Saragosti J., Siberzan P., Buguin A. 2012. Modeling *E. coli* tumbles by rotational diffusion. Implications for chemotaxis. PLoS One 7(4):e35412. [available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3329434/).

[^Berg1972]: Berg HC, Brown DA. 1972. Chemotaxis in Escherichia coli analysed by three-dimensional tracking. Nature. [Available online](https://www.nature.com/articles/239500a0)

[^Baker2005]: Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)


[Next module](../coronavirus/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
