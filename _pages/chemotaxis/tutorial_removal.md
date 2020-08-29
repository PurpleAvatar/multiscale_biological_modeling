---
permalink: /chemotaxis/tutorial_removal
title: "Down gradient/Removal"
sidebar: 
 nav: "chemotaxis"
---

In this page, we will:
 - Simulate cellular response when traveling down the gradient.

## Traveling down the gradient

We have simulated how CheY-P changes when the cell is moving up the attractant gradient. At the higher concentration the cell adapted to, methylation states are changed so that they can compensate for the more ligand-receptor binding to restore the CheY-P value. What if the ligands are removed? Along with increased CheY-P because the cell need to tumble more to "escape" from the wrong direction, we should see methylation states restore to the states before the addition of ligands.

The simulation can be downloaded here: <a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/removal.bngl" download="removal.bngl">removal.bngl</a>

First create a copy of the adaptation model `adaptation.bngl`, name it `removal.bngl`.

To simulate the removal of ligand, or the traveling down the gradient, we will add a "fake reaction" that the ligand disappear with a certain rate. Add this rule within the `reaction rules` section.

	#Simulate ligand removal
	LigandGone: L(t) -> 0 k_gone

In `parameters` section, we define the `k_gone` to be 0.3 first and thus d[L]/dt = -0.3[L]. The concentration can be represented as [L] = 10<sup>7</sup>e<sup>-0.3t</sup>. We will also change the initial ligand concentration to be 1e7. Thus, the concentration of ligand becomes so low that ligand-receptor binding reaches 0 within 50 seconds.

		k_gone 0.3
		L0 1e7

We will set the initial concentrations of all `seed species` to be the final concentrations of the simulation result for our `adaptation.bngl` model, and see if our simulation can restore them to the inital concentrations of the `adaptation.bngl` model. 

First go to the `adaptation.bngl` model, and set `L0` as `1e7`. Also include concentration of each combination of methylation state and ligand binding state of the receptor complex as `observables`. (Concentration of other sepcies are already restored to original state, like CheY-P). Run the simulation. Go to `RuleBender-workspace/PROJECT_NAME/results/adaptation/` and find the simulation result at the final time point. 

Input those concentrations to the `seed species` section of our `removal.bngl` model.

	begin seed species
		@EC:L(t) L0
		@PM:T(l!1,r,Meth~A,Phos~U).L(t!1) 1190
		@PM:T(l!1,r,Meth~B,Phos~U).L(t!1) 2304
		@PM:T(l!1,r,Meth~C,Phos~U).L(t!1) 2946
		@PM:T(l!1,r,Meth~A,Phos~P).L(t!1) 2
		@PM:T(l!1,r,Meth~B,Phos~P).L(t!1) 156
		@PM:T(l!1,r,Meth~C,Phos~P).L(t!1) 402
		@CP:CheY(Phos~U) CheY0*0.71
		@CP:CheY(Phos~P) CheY0*0.29
		@CP:CheZ() CheZ0
		@CP:CheB(Phos~U) CheB0*0.62
		@CP:CheB(Phos~P) CheB0*0.38
		@CP:CheR(t) CheR0
	end seed species

The simulation can also be downloaded here: <a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/removal.bngl" download="removal.bngl">removal.bngl</a>

**STOP:** Go to `simulation` and click `Run`. What happens to CheY phosphorylation? Compare the steady state concentration of each methylation states, are they restored to the level before adding ligands to the `adaptation.bngl` model?
{: .notice--primary}

**STOP:** Similar to what we did for up gradient, we can try different values for `k_gone`. Change `t_end` in the `simulate` method to 1800 seconds, and simulate with `k_gone` = 0.01, 0.03, 0.05, 0.1, 0.3, 0.5.
{: .notice--primary}

All simulation results are stored in the `RuleBender-workspace/PROJECT_NAME/results/MODEL_NAME/TIME/` directory in your computer. Rename the directory with the `k_gone` values instead of the time of running for simplicity. 

We will use Jupyter notebook to visualize the results. Download 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/plotter_down.ipynb" download="plotter_down.ipynb">plotter_down.ipynb</a>

First specify the directories, model name, species of interest, and rates. Put the `RuleBender-workspace/PROJECT_NAME/results/MODEL_NAME/` folder inside the same directory as the Jupyter notebook or change the `model_path`.

~~~ python
	model_path = "removal"  #The folder containing the model
	model_name = "removal"  #Name of the model
	target = "phosphorylated_CheY"    #Target molecule
	vals = [0.01, 0.03, 0.05, 0.1, 0.3, 0.5]  #Gradients of interest
~~~

The second code block will load simulation result at each time point from the `.gdat` file, which stores concentration of all `observables` at all steps, and plot them.

**STOP:** Run the code blocks. How does `k_gone` impact the CheY-P concentrations? Why? Are the tumbling frequencies restored to the background frequency?
{: .notice--primary}



[^Krembel2015]: Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)




[Back to Main Text](home_gradient){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}




