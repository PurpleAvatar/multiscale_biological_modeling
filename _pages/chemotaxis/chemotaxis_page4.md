---
permalink: /chemotaxis/tutorial_gradient
title: "Up gradient/Addition"
sidebar: 
 nav: "chemotaxis"
---

In this page, we will:
 - Simulate cellular response when traveling up the gradient.

### Traveling up the gradient

We've built a model simulating the response of *E. coli* in response to a one-time addition of attractant. However, in real life, the bacterium doesn't suddenly drop into an environment with more attractants; instead, it searches the space to find the gradient. To mimic this phenomenon, we will gradually increase the ligand concentration in the environment, simulating the bacteria moving up the attractant gradient.

First create a copy of the adaptation model `adaptation.bngl`, name it `addition.bngl`.

We will simulate this increase in attractant concentration simply with a "fake reaction" that one ligand molecule becomes two through time. We will add the following reaction to the `reaction rules` section.

	#Simulate exponentially increasing gradient
	LAdd: L(t) -> L(t) + L(t) k_add

In `parameters` section, we define the rate of ligand increase. We will try a rate 0.1/s first. In this case d[L]/dt = 0.1[L]. (You can add `L()` as part of your observables to see how the amount of ligand changed; but since it increases exponentially, seeing other concentrations would be hard) We will also simulate other rate of ligand increase later. We will also change initial ligand amount to 1e4 (too many/few ligands makes increase in ligand concentration too fast/slow), but you can try other values too.

	k_add 0.1
	L0 1e4

Go to `simulation` and click `Run`. 

![image-center](../assets/images/chemotaxis_tutorial_addition01.png){: .align-center}

You will observe that CheY phosphorylation drops gradually first, instead of the instantaneous sharp drop as we add lots of ligand at once. This is because the ligand-receptor binding increases much slower than before. Although our ligand concentration keeps increasing (reaching 1e49 at 1000s), once the receptors are saturated, no more response can be observed.

To compare the results for different increase rate easier, let's get the simulated trajectories for CheY-P. 

Go to the `Navigator` on the left side of the screen, and go to the results folder of your model. Your results for each simulation are stored in the folder named by the time you run, under folder with the same name as your model. In my case, it is in `chemotaxis_from_scratch/results/addition/2020-08-01_18-53-07`. The `.gdat` file stores values at each time point for each of your observable, and `.cdat` stores that of all species.

![image-center](../assets/images/chemotaxis_tutorial_addition02.png){: .align-center}

Let's try different values for k_add: 0.01, 0.03, 0.05, 0.1, 0.3, 0.5. We will get the `.gdat` file for each of the simulations. All simulation results are stored in the `RuleBender-workspace` folder in your computer. In my case, the results are in `RuleBender-workspace/chemotaxis_from_scratch/results/addition/`. I will rename each folder name with the `k_add` values for simplicity.

We will write a short Python script to load and visualize the concentrations of CheY-P through the simulations.
**TODO: put the downloadable here**

~~~Python
import numpy as np
import sys
import os
import matplotlib.pyplot as plt
import colorspace

model_path = sys.argv[1] #name of the .bngl model
model_name = sys.argv[2]
target = sys.argv[3]     #The name of the molecule to plot
vals = sys.argv[4:]      #Rates, also name of the folders

#Define the colors to use
colors = colorspace.qualitative_hcl(h=[0, 300.], c = 60, l = 70, pallete = "dynamic")(len(vals))


def load_data(val):
	file_path = os.path.join(model_path, val, model_name + ".gdat")
	with open(file_path) as f:
		first_line = f.readline() #Read the first line
	cols = first_line.split()[1:] #Get the col names (species names)

	ind = 0
	while cols[ind] != target:
		ind += 1                  #Get col number of target molecule

	data = np.loadtxt(file_path)  #Load the file
	time = data[:, 0]             #Time points
	concentration = data[:, ind]  #Concentrations

	return time, concentration


def plot(val, time, concentration, ax, i):
	legend = "rate: " + str(val)
	ax.plot(time, concentration, label = legend, color = colors[i])
	ax.legend()

	return


def main():
	fig, ax = plt.subplots(1, 1)
	for i in range(len(vals)):
		val = vals[i]
		time, concentration = load_data(val)
		plot(val, time, concentration, ax, i)

	plt.xlabel("time")
	plt.ylabel("concentration (#molecules)")
	plt.title("Active CheY vs time")
	ax.minorticks_on()
	ax.grid(b = True, which = 'minor', axis = 'both', color = 'lightgrey', linewidth = 0.5, linestyle = ':')
	ax.grid(b = True, which = 'major', axis = 'both', color = 'grey', linewidth = 0.8 , linestyle = ':')

	plt.show()



if __name__=='__main__':
	main()
~~~

Run 

	python3 plotter.py [model path] [model name] [target species name] [concentrations]

In my case, I will run

	python3 plotter.py ~/RuleBender-workspace/chemotaxis_from_scratch/results/addition/ addition ActiveCheY 0.01 0.03 0.05 0.1 0.3 0.5

We will see how the CheY-P changes through time for different rates of ligand increases. 

![image-center](../assets/images/chemotaxis_tutorial_addition03.png){: .align-center}

The slower the rate of ligand increasing, the slower receptor binding increases, and the more moderate CheY-P drop becomes. In the end, the high abundances of ligand make all receptors satruate, so that the cells no longer see any gradient, and they adapt to the higher concentration by restoring CheY-P to the original concentration. 

In the next page, we will simulate the case when the cell is moving down the attractant gradient!



[Back to Main Text](home){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}

