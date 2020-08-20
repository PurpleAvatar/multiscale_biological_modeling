---
permalink: /chemotaxis/tutorial_lr
title: "Getting Start and Modeling Steady State"
sidebar: 
 nav: "chemotaxis"
---

This set of tutorials will gradually build a chemotaxis simulation with [BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) at the molecular level from scratch.

In this page, we will:
 - Set up BioNetGen
 - Start to model ligand-receptor dynamics in BNG
 - Explore several key aspects of BNG modeling: rules, species, simulation method, and parameters
 - Model the steady state of ligand-receptor dynamics

## So, what is BioNetGen?

[BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) (BNG) is a software for specification and simulation of rule-based modeling. The chemotaxis pathyway is essentially a set of rules that can specify a set of mathematical equations of concentration of molecules, and we would like to translate it into a simulation. We can specify our rules in [BNG](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409), run the simulation, and visualize the results easily. 

## Set-up

[RuleBender](https://github.com/RuleWorld/rulebender/releases/tag/RuleBender-2.3.2) is the graphical interface for BioNetGen. Please [download](https://github.com/RuleWorld/rulebender/releases/tag/RuleBender-2.3.2) the version corresponding to your operating system. Here is a step-by-step [installation guide](https://github.com/RuleWorld/rulebender/blob/master/docs/RuleBender-installation-guide.pdf).

## Starting with Ligand-Receptor Dynamics

You can download the simulation file here: 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/ligand_receptor.bngl" download="ligand_receptor.bngl">ligand_receptor.bngl</a>

To begin with, let's build a model to simulate ligand-receptor binding dynamics. In our system, there are only two types of molecules: the ligand (L), and the receptor (a receptor complex in our chemotaxis system, and often abbreviated as T). The ligand can bind to the receptor, forming an intermediate, and they could also dissociate. We write this reaction as `L + T <-> L.T`, where the formation of intermediate is **forward reaction**, and its dissociation is **reverse reaction**.

In our system, the number of free ligand and free receptor will drop quickly at the beginning of the simulation, because free ligands and free receptors are readily to meet each other. After a while, there will be more `L.T` in the system and there for more dissociation; at the same time, because free `L` and `T` are less abundant, less binding happens. Therefore, the system will gradually reach an equilibrium where rate of `L` and `T` binding equilibrate with `L.T` dissociation.
- We can write the rate of forward reaction as *k_lr_bind[L][T]*, where *k_lr_bind* is a constant.
- We can write the rate of reverse reaction as *k_lr_dis[L.T]*, where *k_lr_dis* is a constant.
- Equilibrium is reached when *k_lr_bind[L][T] = k_lr_dis[L.T]*.

We will simulate this steady state.

First, open RuleBender. Select "New BioNetGen Project" under File. Since we are going to build from scratch, we can start with blank files. Feel free to start with any existing template too. Call it `chemotaxis_from_scratch`.
![image-center](../assets/images/chemotaxis_tutorial1.png){: .align-center}

Rename your `.bngl` file as `ligand_receptor.bngl`. Now you should be able to start coding at line 1.

![image-center](../assets/images/chemotaxis_tutorial2.png){: .align-center}

## Specifying molecule types

We will walk through all code, but for your reference, BNG documentation can be found [here](http://comet.lehman.cuny.edu/griffeth/BioNetGenTutorialFromBioNetWiki.pdf).

We would like to tell BNG the rules for our model. To specify our model, specify the `begin model` and `end model`. We will add all model specification information between the two lines. We would also like to add our molecules to the model under the `molecule types` section. The `(t)` specifies that molecule `L` contains one component: the binding site with `T`. Same for `T`, the `(l)` specifies the component binding to `L`. We will use this component for L-R binding later.
	
	begin model

	begin molecule types
		L(t)
		T(l)
	end molecule types

	end model

## Specifying reaction rules

BNG reaction rules are written similar as a chemical equation. Left-hand-side are the reactants, which is followed by a unidirectional or bidirectional arrow, indicating uni/bi-directional reaction, and on the right-hand-side are the products. After that, indicate the rate of reaction; and if bi-directional, separate forward and backward reaction rates with a comma. For example, to code up A + B <-> C with forward rate k1, reverse rate k2, we can write `A + B <-> C k1, k2`.

Now let's also add reaction rules within the model. At the left-hand-side, by specifying `L(t)`, we select only unbound `L` molecules; if we would like to select any molecule, we can simply write `L`. At the right-hand-side of the reaction, `L(t!1).T(l!1)` indicates the formation of the intermediate. In BNG, `!` indicates formation of a bond; and a unique character specifies each bond type. We will denote this bond as `!1`. Since the reaction is bidirectional, we will use `k_lr_bind` to denote the rate of forward reaction, and `k_lr_dis` to denote the rate of reverse reaction. *Note: if you compile now, an error will occur because we haven't define parameters yet.*

	begin reaction rules
		LigandReceptor: L(t) + T(l) <-> L(t!1).T(l!1) k_lr_bind, k_lr_dis
	end reaction rules

We can specify how many molecules we would like to put at the beginning of the simulation within `seed species` section. We are putting L0 unbound L molecules, and T0 unbound T molecules at the beginning.

	begin seed species
		L(t) L0
		T(l) T0
	end seed species


## Specifying parameters

Now let's declare all the parameters we mentioned __before__ any usage of them (here, before the `reaction rules` section). BNG is unitless. For simplicity, we will use the number of molecule per cell for all cellular components. The reaction rates are conventionally in the unit of M/s.

Because of the molecules/cell and the M/s units, we need to do some unit conversion here. The volume of *E. coli* is approximately 1µm^3, so our molecule counts are of unit num_molecule/µm^3. One mole of molecule is approximately 6.02 * 10^23 molecules (Avogadro's number), so the unit M is approximately 6.02 * 10^23 molecules/L, which is about 6.02 * 10^8 molecules/µm^3. We record this as NaV. For bimolecular reactions, the rate constant should have unit (M^-1)(s^-1), and we devide NaV to convert to ((molecules/µm^3)^-1)(s^-1). For monomolecular reactions, the rate constant have unit (s^-1), so no unit conversion is required.

Although the specific numbers of cellular components vary between each bacterium, the components in chemotaxis pathway follows a relatively constant ratio. For all the simulations in this set of tutorials, we assign the initial number for each molecule and reaction rates by first deciding a reasonable range based on *in vivo* quantities [^Li2004][^Spiro1997][^Stock1991] and then tuning to fit the model.

	begin parameters
		NaV 6.02e8    #Unit conversion M -> #/µm^3
		L0 1e4        #number of ligand molecules
		T0 7000       #number of receptor complexes
		k_lr_bind 8.8e6/NaV   #ligand-receptor binding
		k_lr_dis 35            #ligand-receptor dissociation
	end parameters

If you save the file now, you should be able to see a Contact-Map indicating the potential bonding of L and T at the upper right corner of your graphical user interface. A contact map can be a help visualization of reaction rules we have, showing the species in the system and interacting species.

![image-center](../assets/images/chemotaxis_tutorial3.png){: .align-center}

Before simulating our model, we would also like to define the observables under `observables` section within the model specification. 

	begin observables
		Molecules L_free L(t)
		Molecules L_bound L(t!1).T(l!1)
	end observables

## Specifying simulation commands

And now we are ready to simulate. Add the `generate network` and `simulate` command outside of your model specification. We will specify three arguments:

**Method**. We will use `method=>"ode"` in all the tutorials, but you could also try `method=>"ssa"`. We will expand on that later. Note that `method=>"ssa"` will be slower for models that are more complex, because it simulates every reaction event while ode only cares about concentrations at each time step.

**Time span**.`t_end`, the simulation duration. BNG simulation time is unitless; for simplicity we define all time units to be second.

**Number of Steps**. `n_steps` tells the program to break the simulation into how many time points to report the concentration.

	generate_network({overwrite=>1})
	simulate({method=>"ode", t_end=>1, n_steps=>100})

The whole simulation code for ligand-receptor dynamics (you can also download here: 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/ligand_receptor.bngl" download="ligand_receptor.bngl">ligand_receptor.bngl</a>)

	begin model

	begin molecule types
		L(t)
		T(l)
	end molecule types

	begin parameters
		NaV 6.02e8    #Unit conversion to cellular concentration M -> #/µm^3
		L0 1e4        #number of ligand molecules
		T0 7000       #number of receptor complexes
		k_lr_bind 8.8e6/NaV    #ligand-receptor binding
		k_lr_dis 35            #ligand-receptor dissociation
	end parameters

	begin reaction rules
		LigandReceptor: L(t) + T(l) <-> L(t!1).T(l!1) k_lr_bind, k_lr_dis
	end reaction rules

	begin seed species
		L(t) L0
		T(l) T0
	end seed species

	begin observables
		Molecules L_free L(t)
		Molecules L_bound L(t!l).T(l!l)
	end observables

	end model

	generate_network({overwrite=>1})
	simulate({method=>"ssa", t_end=>1, n_steps=>100})

**STOP** How would the concentration of free ligand and bound ligand change through 1 seconds?
{: .notice--primary}

Go to `Simulation` at the right side of the Contact Map button and click `Run`. You can visualize your `.gdat` data.

![image-center](../assets/images/chemotaxis_tutorial4.png){: .align-center}

Also try `method=>"ssa"`.

![image-center](../assets/images/chemotaxis_tutorial4_ssa.png){: .align-center}

Observe that, after a period of fast reaction, the concentrations reach to a steady state.

If you are interested, a more detailed tutorial on BNG modeling can be found [here](http://comet.lehman.cuny.edu/griffeth/BioNetGenTutorialFromBioNetWiki.pdf).

[^Li2004]: Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^Stock1991]: Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^Spiro1997]: Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).

[^Schwartz14]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 14.1. 

[^Schwartz17]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 17.2.


[Back to Main Text](home_signal){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}



