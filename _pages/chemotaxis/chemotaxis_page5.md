---
permalink: /chemotaxis/tutorial_gradient
title: "Down gradient/Removal"
sidebar: 
 nav: "chemotaxis"
---

In this page, we will:
 - Simulate cellular response when traveling down the gradient.

### Traveling down the gradient

We have simulated how CheY-P changes when the cell is moving up the attractant gradient. At the higher concentration the cell adapted to, methylation states are changed so that they can compensate for the more ligand-receptor binding to restore the CheY-P value. What if the ligands are removed? Along with increased CheY-P because the cell need to tumble more to "escape" from the wrong direction, we should see methylation states restore to the states before the addition of ligands.

First create a copy of the adaptation model `adaptation.bngl`, name it `removal.bngl`.

To simulate the removal of ligand, or the traveling down the gradient, we will add a "fake reaction" that the ligand disappear with a certain rate. Add this rule within the `reaction rules` section.

	#Simulate ligand removal
	LigandGone: L(t) -> 0 k_gone

In `parameters` section, we define the `k_gone` to be 0.3 first and thus d[L]/dt = -0.3[L]. We will also change the initial ligand concentration to be 1e7.

		k_gone 0.3
		L0 1e7

We will set the initial concentrations of all `seed species` to be the final concentrations of the simulation result for our `adaptation.bngl` model, and see if our simulation can restore them to the inital concentrations of the `adaptation.bngl` model. 

First run the `adaptation.bngl` model with `L0` set as `1e7` and all the `seed species` we need also as `observables`. 

First go to the `adaptation.bngl` model, and set `L0` as `1e7`. Also include concentration of each combination of methylation state and ligand binding state of the receptor complex as `observables`. (Concentration of other sepcies are already restored to original state, like CheY-P). Run the simulation. Go to `RuleBender-workspace/chemotaxis_from_scratch/results/adaptation/` and find the simulation result at the final time point. 

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

We should observe the increase in CheY-P followed by restoration of CheY-P. This is consitent with experimental observations[^1] We should also observe the `TA, TB, TC` restores to the original state of `adaptation.bngl`.

![image-center](../assets/images/chemotaxis_tutorial_removal01.png){: .align-center}

Similar to what we did for up gradient, we can try different values for `k_gone`. Change `t_end` in the `simulate` method to 1800 seconds, and simulate with `k_gone` = 0.01, 0.03, 0.05, 0.1, 0.3, 0.5.

Use the plotting script we used for addition. Run 

	python3 plotter.py [model path] [model name] [target species name] [concentrations]

In my case, I will run

	python3 plotter.py ~/RuleBender-workspace/chemotaxis_from_scratch/results/removal/ removal ActiveCheY 0.01 0.03 0.05 0.1 0.3 0.5

We will see how the CheY-P changes through time for different rates of ligand decreases. 

![image-center](../assets/images/chemotaxis_tutorial_removal02.png){: .align-center}





[^1] Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)




[Previous](tutorial_gradient){: .btn .btn--primary .btn--x-large} [Next Page](home){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}




