---
permalink: /chemotaxis/tutorial_walk
title: "Chemotactic random walk"
sidebar: 
 nav: "chemotaxis"
---

In this page, we will:
 - Simulate *E. coli* chemotaxis at a cellular level
 - Compare performances of different default tumbling frequencies.

## Modeling chemotaxis behavior at a cellular level

Please download the simulation and visualization here: <a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/chemotaxis_walk.ipynb" download="chemotaxis_walk.ipynb">chemotaxis_walk.ipynb</a>. Detailed explanation of the model and each functions can be found in the file too.

Our model will be based on observations from BNG simulation and *E. coli* biology. 

Ingredients and simplifying assumptions of the model:
 - Run. The background average duration of each run (`time_exp`) is a variable of interst. When the cell senses concentration change, the cell changes the expected run duration (`exp_run_time`). The duration of each run follows an exponential distribution with mean = `exp_run_time`. 
 - Tumble. The duration of cell tumble follows an exponential distribution with mean 0.1s[^Saragosti2012]. When it tumbles, we assume it only changes the orientation for the next run but doesn't move in space. The degree of reorientation has a mean of 68° and standard deviation of 36°[^Berg1972]. 
 - Response. As we've seen in the BNG model, the cell can respond to the gradient change within 0.5 seconds. In this model, we allow cells to re-measure the concentration after it runs for 0.5 seconds.
 - Gradient. We model an exponential gradient centered at [1200, 1200] with a concentration of 10^8.5. All cells start at [0, 0], which has a concentration of 10^2. The receptors saturate at a concentration of 10^8. 
 - Performance. The closer to the center of the gradient the better. We could say the cell successfully reaches the target if at the end of the simulation it is at a position with concentration >= 10^8.

 Please makes sure have dependencies installed:
 - [Jupyter Notebook](https://jupyter.org/index.html)
 - [Python3](https://www.python.org/downloads/), version 3.6+
 - [Numpy](https://numpy.org/install/)
 - [Matplotlib](https://matplotlib.org/users/installing.html)
 - [Colorspace](https://python-colorspace.readthedocs.io/en/latest/installation.html) (simply [install with pip](https://pypi.org/project/colorspace/) works too)

First import all dependencies.

~~~ python
import numpy as np
import matplotlib.pyplot as plt
import math
from matplotlib import colors
from matplotlib import patches
import colorspace
~~~

Then we will specify all the model parameters, including mean tumble time 0.1s[^Saragosti2012], mean 68° and std 36° for reorientation[^Berg1972], cell speed of 20µm/s[^Baker2005], and parameters for our ligand concentration gradient. Set a seed for random numbers for reproducibility.

~~~ python
SEED = 128  #Any random seed
np.random.seed(SEED)

#Constants for E.coli tumbling
tumble_angle_mu, tumble_angle_std = 2 * math.pi * 68 / 360, 2 * math.pi * 36 / 360
tumble_time_mu = 0.1

#E.coli movement constants
speed = 20         #um/s, speed of E.coli movement
sec_per_step = 0.5 #Able to respond every 0.5 second
step_size, step_per_sec = speed * sec_per_step, 1.0 / sec_per_step

#Model constants
start = [0, 0]  #All cells start at [0, 0]
ligand_center = [1200, 1200] #Position of highest concentration
center_exponent, start_exponent = 8.5, 2
origin_to_center = 0 #will be actually calculated later
saturation_conc = 10 ** 8 #From BNG model
~~~

For each point on our 2D plane, the concentration can be calculated with an exponential distribution centered at `ligand_center = [1200, 1200]` with concentration = 1e8.5; origin `start = [0, 0]` has concentration 1e2. The exponent has a linear relationship with the distance to the center.

~~~ python
# Calculates Euclidean distance between point a and b
def euclidean_distance(a, b):
    return math.sqrt((a[0] - b[0]) ** 2 + (a[1] - b[1]) ** 2)
# Exponential gradient, the exponent follows a linear relationship with distance to center
def calc_concentration(pos):
    dist = euclidean_distance(pos, ligand_center)
    exponent = (1 - dist / origin_to_center) * (center_exponent - start_exponent) + start_exponent
    
    return 10 ** exponent
~~~

The run duration follows an exponential distribution with `exp_run_time`. When no gradient is present, `exp_run_time` = `time_exp`. When there is a change in ligand concentration, `exp_run_time` changes accordingly. The change is calculated as `(curr_conc - past_conc) / past_conc` to normalize for the exponential gradient. We model this response with `exp_run_time` = `time_exp` + 10 * `change`.

~~~ python
# Calculate the wait time for next tumbling event
def run_time(curr_conc, past_conc, position, time_exp):
        
    curr_conc = min(curr_conc, saturation_conc) #Can't detect higher concentration if receptors saturates
    past_conc = min(past_conc, saturation_conc)
    change = (curr_conc - past_conc) / past_conc #proportion change in concentration
    exp_run_time = time_exp * (1 + 10 * change)
    
    #print(exp_run_time, curr_conc, past_conc, position)
    
    if exp_run_time < 0.000001:
        exp_run_time = 0.000001 #positive wait times
    elif exp_run_time > 4 * time_exp:
        exp_run_time = 4 * time_exp     #the decrease to tumbling frequency is only to a certain extent
    curr_run_time = np.random.exponential(exp_run_time)
    
    return curr_run_time
~~~

The duration of cell tumble follows an exponential distribution with mean 0.1s[^Saragosti2012]. When it tumbles, we assume it only changes the orientation for the next run but doesn't move in space. The degree of reorientation follows a uniform distribution with mean 68 and std 36[^Berg1972]. Also return the horizontal and vertical movement of the cell for the following run.

~~~ python
# Horizontal and Vertical movement of tumbling
def tumble_move(curr_dir):
    #Sample the new direction
    new_dir = np.random.normal(loc = tumble_angle_mu, scale = tumble_angle_std)
    new_dir *= np.random.choice([-1, 1])
    new_dir += curr_dir
    
    if new_dir > 2 * math.pi:
        new_dir -= 2 * math.pi #Keep within [0, 2pi]
        
    move_h = math.cos(new_dir) #Horizontal displacement for next run
    move_v = math.sin(new_dir) #Vertical displacement for next run
    
    tumble_time = np.random.exponential(tumble_time_mu) #Length of the tumbling
    
    return new_dir, move_h, move_v, tumble_time
~~~

Simulation through time for all `time_exp` of all cells.

For each cell, simulate through time as the following pseudocode:

	while `t` < duration:
		Assess the current concentration
		Update current run duration `curr_run_time` and whether it is up/down gradient
		If `curr_run_time` < 0.5s:
	    	run for `curr_run_time` second along current direction
	    	Sample the duration of tumble `tumble_time` and the resulted direction
	    	increment t by `curr_run_time` and `tumble_time`
		If `curr_run_time` > 0.5s:
	    	run for 0.5s along current direction
	    	increment `t` by 0.5s (and then the cell will re-assess the new concentration, and decide the duration of next run)

~~~ python
def simulate(num_cells, duration, time_exp):

    path = np.zeros((len(time_exp), num_cells, duration + 1, 2))
    terminals = [[] for i in range(len(time_exp))]

    for freq_i in range(len(time_exp)):
        for rep in range(num_cells):
            # Initialize simulation, direction initialized randomly
            t = 0
            curr_position = np.array(start)
            past_conc = calc_concentration(start) #Initialize concentration
            curr_direction, move_h, move_v, tumble_time = tumble_move(0)

            while t < duration:
                curr_conc = calc_concentration(curr_position)

                #get wait time
                curr_run_time = run_time(curr_conc, past_conc, curr_position, time_exp[freq_i])

                # if run time (r) is within the step (s), run for r second and then tumble
                if curr_run_time < sec_per_step: 
                    curr_position = curr_position + np.array([move_h, move_v]) * speed * curr_run_time
                    curr_direction, move_h, move_v, tumble_time = tumble_move(curr_direction)
                    t += (curr_run_time + tumble_time)
                
                # if r > s, run for r; then it will be in the next iteration
                else:
                    curr_position = curr_position + np.array([move_h, move_v]) * speed * sec_per_step
                    t += sec_per_step

                #record position approximate for integer number of second
                curr_sec = int(t)
                if curr_sec <= duration:
                    path[freq_i, rep, curr_sec] = curr_position.copy()
                    past_conc = curr_conc

            terminals[freq_i].append((path[freq_i, rep, -1]))
    
    return terminals, path
~~~

## Visualizing trajectories

Before assessing the performances of different default tumbling frequencies, let's run simulation for 3 cells for 500 seconds for the different tumbling frequencies to get a rough idea of what their trajectories look like. We will use a range of 10x shorter expected run time (0.1s) to 10x longer expected run time (10s).

~~~ python
duration = 500   #seconds, duration of the simulation
num_steps = duration * step_per_sec
num_cells = 3
origin_to_center = euclidean_distance(start, ligand_center) #Update the global constant
time_exp = [0.1, 0.25, 0.5, 1.0, 2.0, 5.0, 10.0]

terminals, path = simulate(num_cells, duration, time_exp)
~~~

Run the two code blocks for Part2: Visualizing trajectories (1st block simulates, 2nd block is plotter). The background color indicates concentration: white -> red = low -> high; black dot are starting points; red dots are the points they reached at the end of the simulation; colorful small dots represents trajectories (one color one cell): dark -> bright color = older -> newer time points; dark dashed circle is where concentration reaches 1e8.

**STOP:** What do you observe? Pay attention to: 1) are the cells moving up the gradient?; 2) what's the differences between the shape of the trajectories?; 3) within the 500 seconds, which expected run time allow the cells reach the black dashed circle (target)?; 4) after reaching the target, which expected run time allow the cells to stay in/near the circle?
{: .notice--primary}

**STOP:** Can we make a conclusion on which default tumbling frequencies are good yet? If not, why?
{: .notice--primary}

## Comparing performances

Although the cells with same `time_exp` are under the same mechanisms for random walk, randomness introduced large variations among the trajectories. Therefore, simulation with 3 cells are not convincing. To assess the performances, let's simulate with 500 cells for 800 seconds for each of the `time_exp` values.

For 500 cells, visualizing the trajectories will be messy. We will quantitatively measure the performances by the ability to reach the target at the end of the simulation. We will also calculate the average distance to the center at each time step for each of the `time_exp` values.

~~~python3
#Run simulation for 500 cells with different background tumbling frequencies, Plot average distance to highest concentration point
duration = 800   #seconds, duration of the simulation
num_steps = duration * step_per_sec
num_cells = 500
time_exp = [0.1, 0.25, 0.5, 1.0, 2.0, 5.0, 10.0]
origin_to_center = euclidean_distance(start, ligand_center) #Update the global constant
radius_saturation = (1 - ((math.log10(saturation_conc) - start_exponent) / (center_exponent - start_exponent))) * origin_to_center

all_distance = np.zeros((len(time_exp), num_cells, duration)) #Initialize to store results

terminals, paths = simulate(num_cells, duration, time_exp) #run simulation

for freq_i in range(len(time_exp)):
    for c in range(num_cells):
        for t in range(duration):
            pos = paths[freq_i, c, t]
            dist = euclidean_distance(ligand_center, pos)
            all_distance[[freq_i], c, t] = dist

all_dist_avg = np.mean(all_distance, axis = 1)
all_dist_std = np.std(all_distance, axis = 1)
~~~

**STOP:** Before visualizing the average distances at each time step, what do you expect the result to be (based on the trajectories)?
{: .notice--primary}

Run the two code blocks for Part3: Comparing performances (1st block simulates, 2nd block is plotter). Each colored line indicates a `time_exp`, plotting average distances for the 500 cells; the shaded area is standard deviation; grey dashed line is where concentration reaches 1e8.

**STOP:** What do you conclude about their performances?
{: .notice--primary}

**STOP:** Change the value for `duration` and run simulations for `time_exp = [0.25]` only. How long will the cells take to reach near the grey dashed line?
{: .notice--primary}

**STOP:** For all `time_exp`, after some time the average distance flattens. Why for some of the `time_exp` values, it flattens well before reaching the grey dashed line?
{: .notice--primary}


[^Saragosti2012]: Saragosti J., Siberzan P., Buguin A. 2012. Modeling *E. coli* tumbles by rotational diffusion. Implications for chemotaxis. PLoS One 7(4):e35412. [available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3329434/).

[^Berg1972]: Berg HC, Brown DA. 1972. Chemotaxis in Escherichia coli analysed by three-dimensional tracking. Nature. [Available online](https://www.nature.com/articles/239500a0)

[^Baker2005]: Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)


[Back to Main Text](home_gradient){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}



