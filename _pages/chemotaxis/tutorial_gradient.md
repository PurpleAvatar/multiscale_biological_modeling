---
permalink: /chemotaxis/tutorial_gradient
title: "Up gradient/Addition"
sidebar: 
 nav: "chemotaxis"
---

In this page, we will:
 - Simulate cellular response when traveling up the gradient.

## Traveling up the gradient

We've built a model simulating the response of *E. coli* in response to a one-time addition of attractant. However, in real life, the bacterium doesn't suddenly drop into an environment with more attractants; instead, it searches the space to find the gradient. To mimic this phenomenon, we will gradually increase the ligand concentration in the environment, simulating the bacteria moving up the attractant gradient.

The simulation can be downloaded here: <a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/addition.bngl" download="addition.bngl">addition.bngl</a>

First create a copy of the adaptation model `adaptation.bngl`, name it `addition.bngl`.

We will simulate this increase in attractant concentration simply with a "fake reaction" that one ligand molecule becomes two through time. We will add the following reaction to the `reaction rules` section.

	#Simulate exponentially increasing gradient
	LAdd: L(t) -> L(t) + L(t) k_add

In `parameters` section, we define the rate of ligand increase. We will try a reaction rate 0.1/s first with initial concentration 1e4. So the actual gradient the cell experiences is d[L]/dt = 0.1[L]. By integration then differentiation, we get d[L]/dt = 1000e<sup>0.1t</sup> molecules per second. (You can add `L()` as part of your observables to see how the amount of ligand changed; but since it increases exponentially, seeing other concentrations would be hard.) We will also simulate other rate of ligand increase later. Also change initial ligand amount to 1e4 (too many/few ligands makes increase in ligand concentration too fast/slow), but you can try other values too.

	k_add 0.1
	L0 1e4

The simulation can be also downloaded here: <a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/addition.bngl" download="addition.bngl">addition.bngl</a>

**STOP:** Go to `simulation` and click `Run`. What happens to CheY phosphorylation?
{: .notice--primary}

You will observe that CheY phosphorylation drops gradually first, instead of the instantaneous sharp drop as we add lots of ligand at once. That means, with the ligand concentration increases, the cell is able to continuously lower the tumbling frequency. 

Although our ligand concentration keeps increasing (reaching 1e49 at 1000s), once the receptors are saturated, no more response can be observed, so the cell perceives concentrations higher than saturation concentration as a constant concentration. And the cell is still able to adapt to the constant concentration.

**STOP:** Try different values for `k_add`: 0.01, 0.03, 0.05, 0.1, 0.3, 0.5. What do different `k_add` values imply? How does the system respond to the different values - what are some common trends and some differences?
{: .notice--primary}

All simulation results are stored in the `RuleBender-workspace/PROJECT_NAME/results/MODEL_NAME/TIME/` directory in your computer. Rename the directory with the `k_add` values instead of the time of running for simplicity. 

We will use Jupyter notebook to visualize the results. Download 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/plotter_up.ipynb" download="plotter_up.ipynb">plotter_up.ipynb</a>

Please makes sure have dependencies installed:
 - [Jupyter Notebook](https://jupyter.org/index.html)
 - [Python3](https://www.python.org/downloads/), version 3.6+
 - [Numpy](https://numpy.org/install/)
 - [Matplotlib](https://matplotlib.org/users/installing.html)
 - [Colorspace](https://python-colorspace.readthedocs.io/en/latest/installation.html) (simply [install with pip](https://pypi.org/project/colorspace/) works too)

First specify the directories, model name, species of interest, and rates. Put the `RuleBender-workspace/PROJECT_NAME/results/MODEL_NAME/` folder inside the same directory as the Jupyter notebook or change the `model_path`.

~~~ python
	model_path = "addition"  #The folder containing the model
	model_name = "addition"  #Name of the model
	target = "ActiveCheY"    #Target molecule
	vals = [0.01, 0.03, 0.05, 0.1, 0.3, 0.5]  #Gradients of interest
~~~

The second code block will load simulation result at each time point from the `.gdat` file, which stores concentration of all `observables` at all steps, and plot them.

**STOP:** Run the code blocks. How does `k_add` impact the CheY-P concentrations? Why? Are the tumbling frequencies restored to the background frequency?
{: .notice--primary}


[Back to Main Text](home_gradient){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}



