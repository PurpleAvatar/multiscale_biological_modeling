---
permalink: /chemotaxis/tutorial_lr
title: "Getting Start and Modeling Steady State"
sidebar: 
 nav: "chemotaxis"
---

This set of tutorials will gradually build a chemotaxis simulation with [BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) at the molecular level from scratch!

In this page, we will:
 - Set up BioNetGen
 - Start to model ligand-receptor dynamics in BNG
 - Explore several key aspects of BNG modeling: rules, species, simulation method, and parameters
 - Model the steady state of ligand-receptor dynamics

## So, what is BioNetGen?

[BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) (BNG) is a software for specification and simulation of rule-based modeling. The chemotaxis pathyway is essentially a set of rules that can specify a mathematical model, and we would like to translate it into a simulation. We can specify our rules in [BNG](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409), run the simulation, and visualize the results easily. 

## Set-up

[RuleBender](https://github.com/RuleWorld/rulebender/releases/tag/RuleBender-2.3.2) is the graphical interface for BioNetGen. Please [download](https://github.com/RuleWorld/rulebender/releases/tag/RuleBender-2.3.2) the version corresponding to your operating system. Here is a step-by-step [installation guide](https://github.com/RuleWorld/rulebender/blob/master/docs/RuleBender-installation-guide.pdf).

## Starting with Ligand-Receptor Dynamics

To begin with, let's build a model to simulate ligand-receptor binding dynamics. In our system, there are only two types of molecules: the ligand (L), and the receptor (R). The ligand can bind to the receptor, forming an intermediate, and they could also dissociate. We write this reaction as `L + R <-> L.R`.

In our system, the number of free ligand and free receptor will drop quickly at the beginning of the simulation, because free ligands and free receptors are readily to meet each other. After a while, there will be more `L.R` in the system and there for more dissociation; at the same time, because free `L` and `R` are less abundant, less binindg happens. Therefore, the system will gradually reach an equilibrium where rate of `L` and `R` binding equilibrate with `L.R` dissociation.
- We can write the rate of forward reaction as *k1[L][R]*, where *k1* is a constant.
- We can write the rate of reverse reaction as *k2[L.R]*, where *k2* is a constant.
- Equilibrium is reached when *k1[L][R] = k2[L.R]*.

We will simulate this steady state.

First, open RuleBender. Select "New BioNetGen Project" under File. Since we are going to build from scratch, we can start with blank files. Feel free to start with any existing template too. Call it `chemotaxis_from_scratch`.
![image-center](../assets/images/chemotaxis_tutorial1.png){: .align-center}

Rename your `.bngl` file as `ligand_receptor.bngl`. Now you should be able to start coding at line 1!

![image-center](../assets/images/chemotaxis_tutorial2.png){: .align-center}

We would like to tell BNG the rules for our model. To specify our model, specify the `begin model` and `end model`. We will add all model specification information between the two lines. We would also like to add our molecules to the model under the `molecule types` section. The `(r)` specifies that molecule `L` contains one component, same for `R` and we will use this component for L-R binding later. *Don't worry if you get lost, we will show the complete code.*
	
	begin model

	begin molecule types
		L(r)
		R(l)
	end molecule types

	end model

Now let's also add reaction rules within the model. At the left-hand-side (LHS), by specifying `L(r)`, we select only unbound `L` molecules; if we would like to select any molecule, we can simply write `L`. At the right-hand-side (RHS) of the reaction, `L(r!1).R(l!1)` indicates the formation of the intermediate. `!1` indicates formation of bond, we use numerical values to indicate bond types. Since the reaction is bidirectional, we will use `k1` to denote the rate of forward reaction, and `k2` to denote the rate of reverse reaction. *Note: if you compile now, an error will occur because we haven't define k1 and k2 yet.*

	begin reaction rules
		LigandReceptor: L(r) + R(l) <-> L(r!1).R(l!1) k1, k2
	end reaction rules

We can specify how many molecules we would like to put at the beginning of the simulation within `seed species` section. We are putting L0 unbound L molecules, and R0 unbound R molecules at the beginning.

	begin seed species
		L(r) L0
		R(l) R0
	end seed species

Now let's declare all the parameters we mentioned __before__ any usage of them (here, before the `reaction rules` section). BNG is unitless. For simplicity, we will use the number of moles per liter (M) for concentration, and second for time. The numbers here are just for demonstration; we will include biologically realistic values for chemotaxis in the later simulations. Our unit for reaction rate is M/second, and therefore unit for `k1` is (M^-1)(s^-1), and unit for `k2` is s^-1.

	begin parameters
		L0 100      #M
		R0 50       #M
		k1 0.02     #(M^-1)(s^-1)), rate of forward reaction
		k2 0.1      #s^-1, rate of reverse reaction
	end parameters

If you save the file now, you should be able to see a Contact-Map indicating the potential bonding of L and R at the upper right corner of your graphical user interface!

![image-center](../assets/images/chemotaxis_tutorial3.png){: .align-center}

Before simulating our model, we would also like to define the observables under `observables` section within the model specification. 

	begin observables
		Molecules L_free L(r)
		Molecules L_bound L(r!1).R(l!1)
	end observables

And now we are ready to simulate! Add the `generate network` and `simulate` command outside of your model specification. We will specify three arguments:
 - `method`: BNG supports simulation with Ordinary Differential Equation (ODE) and with Stochastic Simulation Algorithm (SSA, also called Gillespie algorithm). The method is passed in as argument `method=>"ode"` or `method=>"ssa"`. 
 	- ODE: When simulating a system, we need to define how the system evolve through time. In *continuous* simulation of chemical reactions, the state of the system can be reported given any point in time. The reactions rules specifies the rate of change for concentration of the involved species, and they are differential equations. For example, d[L]/dt=k2[L.R] - k1[L][R].[^1]
 	- SSA: When simulate the change of the system through time, we define states of the system. Transition can happen between states that differ by one reaction event. We track the *discrete* amount of each reactants and simulate the system via transition of the states[^2]. For example, the state can transit from [#L=100, #R=50, #L.R=0] to [#L=99, #R=49, #L.R=1], with probability determined both by reaction rate k1 and the the number of ways to choose the L and R molecules.[^2] For using SSA, the measurement of abundance of molecules should actually be number of molecule instead of concentration.
 	- We will use `method=>"ode"` in all the tutorials, but you could also try `method=>"ssa"`! Note that `method=>"ssa"` will be slower for models that are more complex.
 - `t_end`, the simulation duration. BNG is unitless; for simplicity we define all time units to be second.
 - `n_steps` tells the program to break the simulation into how many time points to report the concentration.

BNG supports simulation with Ordinary Differential Equation (ODE) and with Stochastic Simulation Algorithm (SSA, also called Gillespie algorithm). `t_end` specify the simulation duration, and `n_steps` tells the program to break the simulation into how many time points to report the concentration.

	generate_network({overwrite=>1})
	simulate({method=>"ode", t_end=>5, n_steps=>100})

The whole simulation code for ligand-receptor dynamics:

	begin model

	begin molecule types
		L(r)
		R(l)
	end molecule types

	begin parameters
		L0 100
		R0 50
		k1 0.02
		k2 0.1
	end parameters

	begin reaction rules
		LigandReceptor: L(r) + R(l) <-> L(r!1).R(l!1) k1, k2
	end reaction rules

	begin seed species
		L(r) L0
		R(l) R0
	end seed species

	begin observables
		Molecules L_free L(r)
		Molecules L_bound L(r!1).R(l!1)
	end observables

	end model

	generate_network({overwrite=>1})
	simulate({method=>"ode", t_end=>5, n_steps=>100})

**STOP:** How would the concentration of free ligand and bound ligand change through the 5 seconds?

Go to `Simulation` at the right side of the Contact Map button and click `Run`. You can visualize your `.gdat` data.

![image-center](../assets/images/chemotaxis_tutorial4.png){: .align-center}

Also try `method=>"ssa"` (assuming we have 50 receptor molecules, 100 ligand molecules instead of 50M and 100M).

![image-center](../assets/images/chemotaxis_tutorial4_ssa.png){: .align-center}

In the next page, we will start adding phosphorylation in our model!

If you are interested, a more detailed tutorial on BNG modeling can be found [here](http://comet.lehman.cuny.edu/griffeth/BioNetGenTutorialFromBioNetWiki.pdf).

[^1]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 14.1. 
[^2]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 17.2.


[Back to Main Text](home){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


