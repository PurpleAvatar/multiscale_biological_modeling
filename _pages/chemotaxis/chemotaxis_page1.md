---
permalink: /chemotaxis/tutorial_lr
title: "Module 1: Title"
sidebar: 
 nav: "chemotaxis"
---

It's actually not difficult to simulate chemotaxis behavior of *E. coli*. We will build a chemotaxis simulation with [BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) at the molecular level from scratch!

### So, what is BioNetGen?

[BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409) (BNG) is a software for specification and simulation of rule-based modeling. The chemotaxis pathyway is essentially a set of rules that can specify a mathematical model, and we would like to translate it into a simulation. We can specify our rules in [BNG](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409), run the simulation, and visualize the results easily. 

### Set-up

[RuleBender](https://github.com/RuleWorld/rulebender/releases/tag/RuleBender-2.3.2) is the graphical interface for BioNetGen. Please [download](https://github.com/RuleWorld/rulebender/releases/tag/RuleBender-2.3.2) the version corresponding to your operating system. Here is a step-by-step [installation guide](https://github.com/RuleWorld/rulebender/blob/master/docs/RuleBender-installation-guide.pdf).

### Starting with Ligand-Receptor Dynamics

To begin with, let's build a model to simulate ligand-receptor binding dynamics. In our system, there are only two types of molecules: the ligand (L), and the receptor (R). The ligand can bind to the receptor, forming an intermediate, and they could also dissociate. We write this reaction as `L + R <-> L.R`.

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

Now let's also add reaction rules within the model. At the left-hand-side (LHS), by specifying `L(r)`, we select only unbound `L` molecules; if we would like to select any molecule, we can simply write `L`. At the right-hand-side (RHS) of the reaction, `L(r!1).R(l!1)` indicates the formation of the intermediate. `!1` indicates formation of bond, we use numerical values to indicate bond types. Since the reaction is bidirectional, we need to specify rate of reaction for both. *Note: if you compile now, an error will occur because we haven't define k1 and k2 yet.*

	begin reaction rules
		LigandReceptor: L(r) + R(l) <-> L(r!1).R(l!1) k1, k2
	end reaction rules

We can specify how many molecules we would like to put at the beginning of the simulation within `seed species` section. We are putting L0 unbound L molecules, and R0 unbound R molecules at the beginning.

	begin seed species
		L(r) L0
		R(l) R0
	end seed species


Now let's declare all the parameters we mentioned __before__ any usage of them (here, before the `reaction rules` section).

	begin parameters
		L0 100
		R0 50
		k1 0.02
		k2 0.1
	end parameters

If you save the file now, you should be able to see a Contact-Map indicating the potential bonding of L and R at the upper right corner of your graphical user interface!

![image-center](../assets/images/chemotaxis_tutorial3.png){: .align-center}

Before simulating our model, we would also like to define the observables under `observables` section within the model specification. 

	begin observables
		Molecules L_free L(r)
		Molecules L_bound L(r!1).R(l!1)
	end observables

And now we are ready to simulate! Add the `generate network` and `simulate` command outside of your model specification. `t_end` specify the simulation duration, and `n_steps` tells the program to break the simulation into how many time points to report the concentration.

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

Go to `Simulation` at the right side of the Contact Map button and click `Run`. You can visualize your `.gdat` data.

![image-center](../assets/images/chemotaxis_tutorial4.png){: .align-center}

In the next page, we will start adding phosphorylation in our model!

If you are interested, a more detailed tutorial on BNG modeling can be found [here](http://comet.lehman.cuny.edu/griffeth/BioNetGenTutorialFromBioNetWiki.pdf).

[Previous](home){: .btn .btn--primary .btn--x-large} [Next Page](tutorial_phos){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


