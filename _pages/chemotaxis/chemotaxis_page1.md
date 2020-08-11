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

You can download the simulation file here: 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/ligand_receptor.bngl" download="ligand_receptor.bngl">ligand_receptor.bngl</a>

To begin with, let's build a model to simulate ligand-receptor binding dynamics. In our system, there are only two types of molecules: the ligand (L), and the receptor (a receptor complex in our chemotaxis system, and often abbreviated as T). The ligand can bind to the receptor, forming an intermediate, and they could also dissociate. We write this reaction as `L + T <-> L.T`.

In our system, the number of free ligand and free receptor will drop quickly at the beginning of the simulation, because free ligands and free receptors are readily to meet each other. After a while, there will be more `L.T` in the system and there for more dissociation; at the same time, because free `L` and `T` are less abundant, less binindg happens. Therefore, the system will gradually reach an equilibrium where rate of `L` and `T` binding equilibrate with `L.T` dissociation.
- We can write the rate of forward reaction as *k_lr_bind[L][T]*, where *k_lr_bind* is a constant.
- We can write the rate of reverse reaction as *k_lr_dis[L.T]*, where *k_lr_dis* is a constant.
- Equilibrium is reached when *k_lr_bind[L][T] = k_lr_dis[L.T]*.

We will simulate this steady state.

First, open RuleBender. Select "New BioNetGen Project" under File. Since we are going to build from scratch, we can start with blank files. Feel free to start with any existing template too. Call it `chemotaxis_from_scratch`.
![image-center](../assets/images/chemotaxis_tutorial1.png){: .align-center}

Rename your `.bngl` file as `ligand_receptor.bngl`. Now you should be able to start coding at line 1!

![image-center](../assets/images/chemotaxis_tutorial2.png){: .align-center}

## Specifying molecule types

We would like to tell BNG the rules for our model. To specify our model, specify the `begin model` and `end model`. We will add all model specification information between the two lines. We would also like to add our molecules to the model under the `molecule types` section. The `(t)` specifies that molecule `L` contains one component: the binding site with `R`. Same for `R`, the `(l)` specifies the component binding to `L`. We will use this component for L-R binding later.
	
	begin model

	begin molecule types
		L(t)
		T(l)
	end molecule types

	end model

## Specifying reaction rules

Now let's also add reaction rules within the model. At the left-hand-side, by specifying `L(t)`, we select only unbound `L` molecules; if we would like to select any molecule, we can simply write `L`. At the right-hand-side of the reaction, `L(t!1).R(l!1)` indicates the formation of the intermediate. `!1` indicates formation of bond, we use numerical values to indicate bond types. Since the reaction is bidirectional, we will use `k_lr_bind` to denote the rate of forward reaction, and `k_lr_dis` to denote the rate of reverse reaction. *Note: if you compile now, an error will occur because we haven't define parameters yet.*

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

Because of the molecules/cell and the M/s units, we need to do some unit conversion here. The volume of *E. coli* is approximately 1um^3, so our molecule counts are of unit num_molecule/um^3. One mole of molecule is approximately 6.02 * 10^23 molecules (Avogadro's number), so the unit M is approximately 6.02 * 10^23 molecules/L, which is about 6.02 * 10^8 molecules/um^3. We record this as NaV2. For bimolecular reactions, the rate constant should have unit (M^-1)(s^-1), and we devide NaV2 to convert to ((molecules/um^3)^-1)(s^-1). For monomolecular reactions, the rate constant have unit (s^-1), so no unit conversion is required.

Although the specific numbers of cellular components vary between each bacterium, the components in chemotaxis pathway follows a relatively constant stoichiometry. For all the simulations in this set of tutorials, we assign the initial number for each molecule and reaction rates by first deciding a reasonable range based on *in vivo* stoichiometry [^1][^2][^3] and then tuning to fit the model.

	begin parameters
		NaV2 6.02e8   #Unit conversion to cellular concentration M/L -> #/um^3
		L0 1e4        #number of ligand molecules
		T0 7000       #number of receptor complexes
		k_lr_bind 8.8e6/NaV2   #ligand-receptor binding
		k_lr_dis 35            #ligand-receptor dissociation
	end parameters

If you save the file now, you should be able to see a Contact-Map indicating the potential bonding of L and T at the upper right corner of your graphical user interface!

![image-center](../assets/images/chemotaxis_tutorial3.png){: .align-center}

Before simulating our model, we would also like to define the observables under `observables` section within the model specification. 

	begin observables
		Molecules L_free L(t)
		Molecules L_bound L(t!1).T(l!1)
	end observables


## Specifying simulation commands

And now we are ready to simulate! Add the `generate network` and `simulate` command outside of your model specification. We will specify three arguments:

**Method**. BNG supports simulation with Ordinary Differential Equation (ODE) and with Stochastic Simulation Algorithm (SSA, also called Gillespie algorithm). The method is passed in as argument `method=>"ode"` or `method=>"ssa"`. 
 - ODE: When simulating a system, we need to define how the system evolve through time. In *continuous* simulation of chemical reactions, the state of the system can be reported given any point in time. The reactions rules specifies the rate of change for concentration of the involved species, and they are differential equations. For example, d[L]/dt=k2[L.R] - k1[L][R].[^1]
 - SSA: When simulate the change of the system through time, we define states of the system. Transition can happen between states that differ by one reaction event. We track the *discrete* amount of each reactants and simulate the system via transition of the states[^2]. For example, the state can transit from [#L=100, #T=50, #L.T=0] to [#L=99, #T=49, #L.R=1], with probability determined both by reaction rate k_lr_bind and the the number of ways to choose the L and R molecules.[^2] For using SSA, the measurement of abundance of molecules should actually be number of molecule instead of concentration.
 
 We will use `method=>"ode"` in all the tutorials, but you could also try `method=>"ssa"`! Note that `method=>"ssa"` will be slower for models that are more complex.

**Time span**.`t_end`, the simulation duration. BNG is unitless; for simplicity we define all time units to be second.

**Number of Steps**. `n_steps` tells the program to break the simulation into how many time points to report the concentration.

	generate_network({overwrite=>1})
	simulate({method=>"ode", t_end=>1, n_steps=>100})

The whole simulation code for ligand-receptor dynamics (you can also download here: 
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/downloadable/ligand_receptor.bngl" download="ligand_receptor.bngl">ligand_receptor.bngl</a>)

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

Also try `method=>"ssa"`.

![image-center](../assets/images/chemotaxis_tutorial4_ssa.png){: .align-center}

In the next section, we will start adding phosphorylation in our model!

If you are interested, a more detailed tutorial on BNG modeling can be found [here](http://comet.lehman.cuny.edu/griffeth/BioNetGenTutorialFromBioNetWiki.pdf).

[^1]: Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^2]: Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^3]: Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).

[^4]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 14.1. 

[^5]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 17.2.


[Back to Main Text](home){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
