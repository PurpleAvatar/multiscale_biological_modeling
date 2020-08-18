---
permalink: /chemotaxis/tutorial_phos
title: "Phosphorylation"
sidebar: 
 nav: "chemotaxis"
---

In this page, we will:
 - Add phosphorylation mechanisms for chemotaxis
 - Observe cellular behavior in response to stimuli

## Phosphorylation Mechanisms

![image-center](../assets/images/chemotaxisphosnew.png){: .align-center}
<figcaption>Visualization of pathway for reference.</figcaption>

We have:

**Ligand binding and dissociation**. L + T <-> LT with rate *k_lr_bind, k_lr_dis*.

**Receptor complex autophosphorylation**. The receptor complex is composed of MCPs, CheW, and CheA. CheA undergoes autophosphorylation, and the rate of autophosphorylation depends on conformation of the receptor complex. When receptor is not bound with ligand, autophosphorylation is faster. Note that the phosphoryl group is from an ATP->ADP reaction, but we will just code as phosphorylation states in modeling for simplicity. 
 - T -> T-P    rate *k_T_phos*
 - LT -> LT-P  rate *k_T_phos x 0.2*

**CheY phosphorylation and dephosphorylation**. CheA-P phosphorylates a downstream protein, CheY. Phosphorylated CheY will be responsible for the cellular response (CW rotataion), so we will use the level of CheY-P to indicate the level of cellular response. But if CheY stay phosphorylated forever, the cell will remain in the same actions. So we would also like to include CheZ to catalyze the removal the phosphoryl group from Y-P.
 - T-P + CheY -> T + CheY-P  *k_Y_phos*
 - Z + Y-P -> Z + Y + P *k_Y_dephos*

## Include phosphorylation into the model

You can download the simulation file here: 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/phosphorylation.bngl" download="phosphorylation.bngl">phosphorylation.bngl</a>

First, we introduce `state` in our particles to mark whether it is phosphorylated or not. Change `T(l)` to `T(l,Phos~U~P)`. The `Phos~U~P` indicates we introduce phosphorylation states to `T`, and `U` indicates unphosphorylated, while `P` indicates phosphorylated. You can also use other letters. We also add molecule `CheY(Phos~U~P)` and `CheZ()`. So our molecule definitions become the following.(*Note: be careful with the use of spaces; don't put spaces after the comma.*)

	begin molecule types
		L(t)             #ligand molecule
		T(l,Phos~U~P)    #receptor complex
		CheY(Phos~U~P)
		CheZ()
	end molecule types

And we update the reaction rules with the phosphorylation and dephosphorylation reactions above.

	begin reaction rules
		LigandReceptor: L(t) + T(l) <-> L(t!1).T(l!1) k_lr_bind, k_lr_dis
		
		#Free vs. ligand-bound receptor complexes autophosphorylates at different rates
		FreeReceptorPhos: T(l,Phos~U) -> T(l,Phos~P) k_T_phos
		BoundReceptorPhos: L(t!1).T(l!1,Phos~U) -> L(t!1).T(l!1,Phos~P) k_T_phos*0.2
		
		CheYPhos: T(Phos~P) + CheY(Phos~U) -> T(Phos~U) + CheY(Phos~P) k_Y_phos
		CheYDephos: CheZ() + CheY(Phos~P) -> CheZ() + CheY(Phos~U) k_Y_dephos
	end reaction rules

We need to indicate the number of molecules at each states present at the beginning of the simulation. Since we are adding ligands at the beginnin of the simulation, the fraction of molecules at the same states should be equal to the equilibrium concentration when no ligand is present (we will elaborate on that later).

	begin seed species
		L(t) L0
		T(l,Phos~U) T0*0.8
		T(l,Phos~P) T0*0.2
		CheY(Phos~U) CheY0*0.5
		CheY(Phos~P) CheY0*0.5
		CheZ() CheZ0
	end seed species

Let's update all the parameters based on *in vivo* stoichiometry [^Li2004][^Spiro1997][^Stock1991]. 

	begin parameters
		NaV2 6.02e8   #Unit conversion to cellular concentration M/L -> #/um^3
		L0 0        #number of ligand molecules
		T0 7000       #number of receptor complexes
		CheY0 20000
		CheZ0 6000
		
		k_lr_bind 8.8e6/NaV2   #ligand-receptor binding
		k_lr_dis 35            #ligand-receptor dissociation
		k_T_phos 15           #receptor complex autophosphorylation
		k_Y_phos 3.8e6/NaV2    #receptor complex phosphorylates Y
		k_Y_dephos 8.6e5/NaV2  #Z dephosphoryaltes Y
	end parameters

We would also be interested in the number of T-P and Y-P during the simulation.

	begin observables
		Molecules ActiveY CheY(Phos~P)
		Molecules ActiveT T(Phos~P)
		Molecules L_bound L(t!1).T(l!1)
	end observables

Observe the simulation for longer. Change `t_end` at the bottom to 3. 

	generate_network({overwrite=>1})
	simulate({method=>"ode", t_end=>3, n_steps=>100})

You can also download the simulation file here: 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/phosphorylation.bngl" download="phosphorylation.bngl">phosphorylation.bngl</a>

## Results: cellular responses

Before running the simulation, let's think about what will happen. If we don't add any ligand molecule into the system, then T phosphorylation happens at rate *k_T_phos*, and T will phosphorylates CheY, which will also be dephosphorylated by CheZ. The concentrations of phosphorylated T and CheY will stay at an equilibrium. That's the initial concentrations of molecules at each state we defined earlier. When we add ligand molecules into the system, as there are more bound T, there will be less T-P, and therefore less CheY-P.

Set `L0` in the `parameters` section to 0, and then click `Simulate` and `Run`. You could observe the constant level of R-P and Y-P.

![image-center](../assets/images/chemotaxis_tutorial5.png){: .align-center} 

Then change `L0` to 1e4.

![image-center](../assets/images/chemotaxis_tutorial6.png){: .align-center} 

Then change `L0` to 1e5.

![image-center](../assets/images/chemotaxis_tutorial7.png){: .align-center} 

With the addition of attractants, more receptor dimers are bound to attractants, and therefore less CheA autophosphorylation happens (here we include the CheA as part of the receptor complex). As a result, less CheY can be phosphorylated by CheA, and therefore, CheY phosphorylates the flagellar proteins less frequently, reducing tumbling frequency. 

But this is only half of the story. In the next section, we will code up the adaptation, including CheR, CheB, and methylation states for chemotaxis.



[^Bertoli2013]: Bertoli C, Skotheim JM, de Bruin RAM. 2013. Control of cell cycle transcription during G1 and S phase. Nature Reviews Molecular Cell Biology 14:518-528. [Available online](https://www.nature.com/articles/nrm3629).

[^Li2004]: Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^Stock1991]: Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^Spiro1997]: Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).


[Back to Main Text](home){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}



