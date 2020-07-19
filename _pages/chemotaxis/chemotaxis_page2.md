---
permalink: /chemotaxis/tutorial_phos
title: "Module 1: Title"
sidebar: 
 nav: "chemotaxis"
---

### Adding Phosphorylation

Ligand binding and dissociation should change the conformation of the ligand and therefore impact the downstream reactions. Now let's include more downstream reactions in our model.

- Ligand binding and dissociation: L + R <-> LR with rate \$$k1, k2$$
- Let's say the receptor is a complex of proteins, and one of the protein undergoes autophosphorylation, the rate of autophosphorylation depends on conformation of the receptor. When receptor is not bound with ligand, autophosphorylation is faster.
	- LR + P -> LR-P $k3$
	- R + P -> R-P   $k3 \times 0.2$
- Then the autophosphorylated receptor complex can phosphorylate a downstream protein, call it Y. The phosphorylated Y will be able to some observable cellular response, so we will use the level of Y-P to indicate the level of cellular response later.
	- R-P + Y -> R + Y-P  $k4$
- But if the Y stay phosphorylated forever, the cell will remain in the same actions. So we would also like to include a molecule Z to catalyze the removal the phosphoryl group from Y-P.
	- Z + Y-P -> Z + Y + P $k5$

Now let's include these into our BNG model.

First, we would like introduce `state` in our receptors. Change `R(l)` to `R(l,Phos~U~P)`. The `Phos~U~P` indicates we introduce phosphorylation states to `R`, and `U` indicates unphosphorylated, while `P` indicates phosphorylated. You can also use other letters. We also add molecule `Y(Phos~U~P)` and `Z()`. So our molecule definitions become the following.(*Note: be careful with the use of spaces; don't put spaces after the comma.*)

	begin molecule types
		L(r)
		R(l,Phos~U~P)
		Y(Phos~U~P)
		Z()
	end molecule types

And we update the reaction rules with the phosphorylation and dephosphorylation reactions above.

	begin reaction rules
		LigandReceptor: L(r) + R(l) <-> L(r!1).R(l!1) k1, k2
	
		#Free vs. ligand-bound receptor complexes autophosphorylates at different rates
		FreeReceptorPhos: R(l,Phos~U) -> R(l,Phos~P) k3
		BoundReceptorPhos: L(r!1).R(l!1,Phos~U) -> L(r!1).R(l!1,Phos~P) k3*0.2
	
		YPhos: R(Phos~P) + Y(Phos~U) -> R(Phos~U) + Y(Phos~P) k4
		YDephos: Z() + Y(Phos~P) -> Z() + Y(Phos~U) k5
	end reaction rules

Now let's indicate the number of molecules present at the beginning of the simulation. We will have half of the `R` and half of the `Y` being phosphorylated at the beginning.

	begin seed species
		L(r) L0
		R(l,Phos~U) R0*0.5
		R(l,Phos~P) R0*0.5
		Y(Phos~U) Y0*0.5
		Y(Phos~P) Y0*0.5
		Z() Z0
	end seed species

Let's update all the parameters.

	begin parameters
		L0 100
		R0 50
		Y0 20
		Z0 5
	
		k1 0.02 #ligand-receptor binding
		k2 0.1 #ligand-receptor dissociation
		k3 0.5 #receptor complex autophosphorylation
		k4 0.05 #receptor complex phosphorylates Y
		k5 0.25 #Z dephosphoryaltes Y
	end parameters

We would also be interested in the number of T-P and Y-P during the simulation.

	begin observables
		Molecules L_free L(r)
		Molecules L_bound L(r!1).R(l!1)
		Molecules ActiveR R(Phos~P)
		Molecules ActiveY Y(Phos~P)
	end observables

Observe the simulation for longer. Change `t_end` at the bottom to 20. Now the whole simulation code is like this.

	begin model

	begin molecule types
		L(r)
		R(l,Phos~U~P)
		Y(Phos~U~P)
		Z()
	end molecule types

	begin parameters
		L0 100
		R0 50
		Y0 20
		Z0 5
		
		k1 0.02 #ligand-receptor binding
		k2 0.1 #ligand-receptor dissociation
		k3 0.5 #receptor complex autophosphorylation
		k4 0.05 #receptor complex phosphorylates Y
		k5 0.25 #Z dephosphoryaltes Y
	end parameters

	begin reaction rules
		LigandReceptor: L(r) + R(l) <-> L(r!1).R(l!1) k1, k2
		
		#Free vs. ligand-bound receptor complexes autophosphorylates at different rates
		FreeReceptorPhos: R(l,Phos~U) -> R(l,Phos~P) k3
		BoundReceptorPhos: L(r!1).R(l!1,Phos~U) -> L(r!1).R(l!1,Phos~P) k3*0.2
		
		YPhos: R(Phos~P) + Y(Phos~U) -> R(Phos~U) + Y(Phos~P) k4
		YDephos: Z() + Y(Phos~P) -> Z() + Y(Phos~U) k5
	end reaction rules

	begin seed species
		L(r) L0
		R(l,Phos~U) R0*0.5
		R(l,Phos~P) R0*0.5
		Y(Phos~U) Y0*0.5
		Y(Phos~P) Y0*0.5
		Z() Z0
	end seed species

	begin observables
		Molecules L_free L(r)
		Molecules L_bound L(r!1).R(l!1)
		Molecules ActiveR R(Phos~P)
		Molecules ActiveY Y(Phos~P)
	end observables

	end model

	generate_network({overwrite=>1})
	simulate({method=>"ode", t_end=>20, n_steps=>100})

### So What?

Before running the simulation, let's think about what will happen. If we don't add any ligand molecule into the system, then R phosphorylation happens at rate $k3$, and R will phosphorylates Y, which will also be dephosphorylated by Z. The concentrations of phosphorylated R and Y will stay at an equilibrium - actually conveniently the 50\% phosphorylated we defined in the `seed species` section. When we add ligand molecules into the system, as there are more bound R, there will be less R-P, and therefore less Y-P.

Change `L0` in the `parameters` section to 0, and then click `Simulate` and `Run`. You could observe the constant level of R-P and Y-P.

![image-center](../assets/images/chemotaxis_tutorial5.png){: .align-center} 

Then change `L0` to 20.

![image-center](../assets/images/chemotaxis_tutorial6.png){: .align-center} 

Then change `L0` to 100.

![image-center](../assets/images/chemotaxis_tutorial7.png){: .align-center} 

Actually, that is similar to the action of chemotaxis! With the addition of attractants, more receptor dimers are bound to attractants, and therefore less CheA autophosphorylation happens (here we include the CheA as part of the receptor complex). As a result, less CheY can be phosphorylated by CheA, and therefore, CheY phosphorylates the flagellar proteins less frequently, reducing tumbling frequency. 

But this is only half of the story. In the next section, we will code up the adaptation, including CheR, CheB , and methylation states for chemotaxis.

If you would like to continue using this model for the next section, rename R to T (T stands for ternary complex, we want to avoid confusion with CheR). You could rename `Y` to `CheY`, `Z` to `CheZ` if you prefer.


[Previous](tutorial_lr){: .btn .btn--primary .btn--x-large} [Next Page](tutorial_adaptation){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
