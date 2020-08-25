---
permalink: /chemotaxis/home_signal
title: "Signaling and Ligand-Receptor Dynamics"
sidebar:
 nav: "chemotaxis"
---

## Signaling Pathway

Chemotaxis is one example of many ways in which an organism must be able to perceive a change in its environment and react accordingly. This response is governed by a process called **signal transduction**, in which the organism identifies an external molecular stimulus and then transmits this stimulus to the interior of the cell in order to effect a response.

Although we did not delve into the details at that time, we have already seen an example of signal transduction when we discussed transcription in the [previous module](motifs/transcription). **Receptor proteins** on the outside of the cell bond with molecules and are able to detect changes in molecular concentration. This "signal" is then "transduced" via a series of internal chemical processes that changes a transcription factor into an active state.

In the case of chemotaxis, *E. coli* has receptor proteins that are able to detect attractants such as glucose by binding to and forming a complex with these **ligands**. In the next two lessons, we will walk through how the cell is able to detect this molecular signal and transduce it internally into a sequence of reactions that lead to a change in the bacterium's movement.

![image-center](../assets/images/chemotaxis_signal.png){: .align-center}
<figcaption>Overview of the signaling pathway of chemotaxis. The red circles represent ligands(L). When ligands bind to receptor, the signal is transduced via a series of enzymes, and finally influences the rotation direction of a flagellum.</figcaption>


## Modeling ligand-receptor dynamics

We will first focus our attention on the process by which a signal is detected and how the environmental concentration of ligands and the number of receptors impacts ligand-receptor binding. Although *E. coli* will have different types of surface receptors that can sense a variety of different attractant/repellent ligands in its environment, we will focus on how to model the binding of a single type of receptor to a single type of ligand.

The chemical reactions that we considered in the previous two modules were **irreversible** (i.e., one-directional). For example, in the prologue, we had a reaction whose reactants were two predator molecules and a prey molecule, and whose reactants were three predator molecules. But we did not have the reverse reaction in which the three predator molecules split into two predator molecules and a prey.

In this chapter, we will encounter **reversible** reactions that proceed continuously in both directions at different rates. If a ligand collides with a receptor, then there is some probability that this will lead to the two molecules bonding into a complex. But at the same time, in any unit of time, there is also a probability that a bound receptor-ligand complex will **dissociate** into two separate molecules. We will discuss what makes two molecules more likely to bond in a future module, but for now, we will assert that the more suited a receptor is to a ligand, the higher the probability of  bonding and the lower the probability of dissociation.

Why should this reaction be reversible? First, surface receptors are typically complicated molecules, and it would be costly to the organism if it needed to keep reproducing these molecules. Second, if complexes dissociate, then a brief signal will not be detected by an organism indefinitely; we will say more about how the cell responds to a changing concentration of ligand over time soon.

For now, we will start building a model of ligand-receptor dynamics. We will represent the receptor molecule by *T*, the ligand molecule by *L*, and the bound complex as *TL*. We have the **forward reaction** *T* + *L* → *TL*, which takes place at some rate *k*<sub>bind</sub>, and the **reverse reaction** *TL* → *T* + *L*, which takes place at some rate *k*<sub>dissociate</sub>. If we start with a free floating supply of *T* and *L* molecules, what will happen?

*TL* will initially be formed quickly at the expense of the free-floating *T* and *L* molecules; the reverse reaction will not occur because of the lack of *TL* complexes. As the concentration of *TL* grows and the concentrations of  *T* and *L* decrease, the rate of increase in *TL* will slow. Eventually, the number of *TL* complexes being formed by the forward reaction will balance the number of *TL* complexes being split apart by the reverse reaction. At this point, called a **steady state** or **equilibrium**, the concentration of all particles will become constant.

## Calculation of steady state concentration in a reversible reaction

In fact, we can calculate the steady state concentrations of *T* and *L* for our reversible reaction.  Suppose that we begin with initial concentrations of *T* and *L* that are represented by *t*<sub>0</sub> and *l*<sub>0</sub>, respectively. Let [*L*], [*T*], and [*LT*] denote the concentrations of the three molecule types. And assume that the reaction rates *k*<sub>bind</sub> and *k*<sub>dissociate</sub> are fixed.

Our goal is to find the steady-state concentration of *LT*. When this occurs, we know that the rate of production of *LT* is equal to the rate of its dissociation; in other words, we know that

*k*<sub>bind</sub> · [*L*] · [*T*] = *k*<sub>dissociate</sub> · [*LT*].

We also know that by the law of conservation of mass, the total number of *L* and *T* molecules is always constant across the system. In particular, the number of these particles is equal to their initial concentrations. That is, at any time point, we have that

[*L*] + [*LT*] = *l*<sub>0</sub>

and that

[*T*] + [*LT*] = *t*<sub>0</sub>.

Solving these equations for [*L*] and [*T*] yields the following two equations:

[*L*] = *l*<sub>0</sub> - [*LT*]<br>
[*T*] = *t*<sub>0</sub> - [*LT*]

We will now substitute the expressions on the right for [*L*] and [*T*] into our original steady-state equation:

*k*<sub>bind</sub> · (*l*<sub>0</sub> - [*LT*]) · (*t*<sub>0</sub> - [*LT*]) = *k*<sub>dissociate</sub> · [*LT*]

Expanding the left side of this equation gives us the following updated equation:

*k*<sub>bind</sub> · [*LT*]<sup>2</sup> - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub>) · [*LT*] +  = *k*<sub>dissociate</sub> · [*LT*] + *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub>

Finally, we subtract the right side of this equation from both sides:

*k*<sub>bind</sub> · [*LT*]<sup>2</sup> - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>) · [*LT*] + *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub> = 0

This equation may look daunting, but most of its components are constants. In fact, the only unknown is [*LT*], which makes this a quadratic equation, or an equation of the form *a* · *x*<sup>2</sup> + *b* · *x* + *c* = 0 for constants *a*, *b*, and *c* and a single unknown *x*. Specifically, for the quadratic equation in terms of [*LT*], we have the constants *a* = *k*<sub>bind</sub>, *b* = - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>), and *c* = *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub>.

The quadratic formula tells us that the equation *a* · *x*<sup>2</sup> + *b* · *x* + *c* = 0  has solutions given by the following equation --- and you thought you'd never use this formula again!

$$x = \dfrac{-b \pm \sqrt{b^2 - 4 \cdot a \cdot c}}{2 \cdot a}$$

**STOP**: Use the quadratic equation to solve for [*LT*] and find the steady-state concentration of *LT*. How can we use it to find the steady-state concentrations of *L* and *T*?
{: .notice--primary}

Now that we have reduced the computation of the steady-state concentration of *LT* to the solution of a quadratic equation, let's compute this steady-state concentration for a sample collection of parameters. We will then change the parameters and see how the steady-state concentration changes.

Say that we are given the following parameter values (the units are not important for this toy example):
* *k*<sub>bind</sub> = 2;
* *k*<sub>dissociate</sub> = 5;
* *l*<sub>0</sub> = 50;
* *t*<sub>0</sub> = 50.

Plugging these values into the seemingly daunting quadratic equation, we obtain the following:

* *a* = *k*<sub>bind</sub> = 2
* *b* = - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>) = -205
*c* = *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub> = 5000

That is, we are solving the equation 2 · [*LT*]<sup>2</sup> - 205 · [*LT*] + 5000 = 0. Using the quadratic formula to solve for [*LT*] gives

$$[LT] = \dfrac{205 \pm \sqrt{205^2 - 4 \cdot 2 \cdot 5000}}{2 \cdot 2} = 51.25 \pm 11.25$$.

It would seem that there are *two* solutions: 51.25 + 11.25 = 62.5 and 51.25 - 11.25 = 40. However, because *l*<sub>0</sub> and *t*<sub>0</sub>, the respective initial concentrations of *L* and *T*, are both equal to 50, we cannot have that the steady-state concentration of *LT* is 62.5; as a result, it must be 40.

Now that we know the steady-state concentration of *LT*, we can recover the values of [*L*] and [*T*]:

[*L*] = *l*<sub>0</sub> - [*LT*] = 10<br>
[*T*] = *t*<sub>0</sub> - [*LT*] = 10

What if the forward reaction is slower? We would imagine that the equilibrium concentration of *LT* would decrease since the reverse reaction will occur faster than the forward reaction. For example, if we change *k* to 1, then we obtain the following adjusted parameter values:

* *a* = *k*<sub>bind</sub> = 1

* *b* = - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>) = -105

* *c* = *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub> = 2500

In this case, if we solve for [*LT*], we obtain [*LT*] = 36.492; the steady-state concentration has decreased as anticipated.

**STOP**: What do you think will happen to the steady-state concentration of *LT* if the initial concentration (*l*<sub>0</sub>) increases or decreases? What if the dissociation rate (*k*<sub>dissociate</sub>) increases or decreases?  Confirm your prediction by changing the parameters above and solving the quadratic formula for [*LT*].
{: .notice--primary}

## Verifying a theoretical steady-state concentration via simulation

In the [previous module](motifs), we saw how to avoid keeping track of the diffusion of individual particles if simulating molecules that are uniformly distributed throughout their environment. The *E. coli* cell is so small that we will assume that the concentration of any particle in its immediate surroundings is uniform. Therefore, let us see if the same type of simulation can replicate the steady-state concentrations that we found above.

Even though we can calculate steady-state concentrations by hand, we will find a simulation useful for two reasons. First, a particle-free simulation will give us snapshots of the system over multiple time points and allow us to see how quickly the concentrations reach equilibrium. Second, we will soon expand our model of chemotaxis to have many more particles and reactions, and direct interpretation of the system will quickly become impossible.

The following tutorial uses [BioNetGen](https://www.csb.pitt.edu/Faculty/Faeder/?page_id=409), which we will use throughout this module to build particle-free simulations of chemotaxis. We start by building a model to determine the equilibrium of a reversible reaction involving ligands and receptors.

[Visit tutorial](tutorial_lr){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Does a simulation confirm our steady-state calculations?

Here we've shown that using BNG and calculating by hand reach the same conclusion for bimolecular reactions.

* SHUANGER: This is where we should return from the tutorial and interpret the results that we found, comparing against the examples that we had before.

From the BNG simulation, we can observe that *L* and *T* drop quickly while *LT* increases quickly at the begining of the simulation, and then reach steady state concentrations. Plug in the model parameters into our quadratic equation, can you calculate the steady state concentrations and obtain the same results?

![image-center](../assets/images/chemotaxis_tutorial4.png){: .align-center}
<figcaption>Concentration plot for ligand-receptor dynamics with ODE simulation. The concentrations reach a steady state at the end of the simulation. </figcaption>

![image-center](../assets/images/chemotaxis_tutorial4_ssa.png){: .align-center}
<figcaption>Concentration plot for ligand-receptor dynamics with SSA simulation.</figcaption>

* Phillip will then need to point the reader to the next section by saying this is just the beginning of the model we will build to study chemotaxis. (And computing steady-state concentration is just a toy example compared to questions we will ask soon.)

[^Munroe]: Randall Munroe. What If? [Available online](https://what-if.xkcd.com/)

[^Pierucci1978]: Pierucci O. 1978. Dimensions of *Escherichia coli* at various growth rates: Model of envelope growth. Journal of Bacteriology 135(2):559-574. [Available online](https://jb.asm.org/content/jb/135/2/559.full.pdf)

[^Sim2017]: Sim M, Koirala S, Picton D, Strahl H, Hoskisson PA, Rao CV, Gillespie CS, Aldridge PD. 2017. Growth rate control of flagellar assembly in *Escherichia coli* strain RP437. Scientific Reports 7:41189. [Available online](https://www.nature.com/articles/srep41189#:~:text=Escherichia%20coli%20is%20a%20prominent,distributed%20across%20the%20cell%20surface.)

[^Baker2005]: Baker MD, Wolanin PM, Stock JB. 2005. Signal transduction in bacterial chemotaxis. BioEssays 28:9-22. [Available online](https://pubmed.ncbi.nlm.nih.gov/16369945/)

[^Weis1990]: Weis RM, Koshland DE. 1990. Chemotaxis in *Escherichia coli* proceeds efficiently from different initial tumble frequencies. Journal of Bacteriology 172:2. [Available online](https://jb.asm.org/content/jb/172/2/1099.full.pdf)

[^Berg2000]: Berg HC. 2000. Motile behavior of bacteria. Physics today 53(1):24. [Available online](https://physicstoday.scitation.org/doi/pdf/10.1063/1.882934)

[^Achouri2015]: Achouri S, Wright JA, Evans L, Macleod C, Fraser G, Cicuta P, Bryant CE. 2015. The frequency and duration of *Salmonella* macrophage adhesion events determines infection efficiency. Philosophical transactions B 370(1661). [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4275903/)

[^Turner2016]: Turner L, Ping L, Neubauer M, Berg HC. 2016. Visualizing flagella while tracking bacteria. Biophysical Journal 111(3):630--639.[Available online](https://pubmed.ncbi.nlm.nih.gov/27508446/)

[^Parkinson2015]: Parkinson JS, Hazelbauer, Falke JJ. 2015. Signaling and sensory adaptation in *Escherichia coli* chemoreceptors: 2015 update. [Available online](https://www.sciencedirect.com/science/article/abs/pii/S0966842X15000578)

[^Yang2019]: Yang W, Cassidy CK, Ames P, Diebolder CA, Schulten K, Luthey-Schulten Z, Parkinson JS, Briegel A. 2019. *In situ* confomraitonal changes of the *Escherichia coli* serine chemoreceptor in different signaling states. mBio. [Available online](https://mbio.asm.org/content/10/4/e00973-19/article-info)

[^Saragosti2001]: Saragosti J, Calvez V, Bournaveas, N, Perthame B, Buguin A, Silberzan P. 2001. Directional persistence of chemotactic bacteria in a traveling concentration wave. PNAS. [Available online](https://www.pnas.org/content/pnas/108/39/16235.full.pdf)

[^Hlavacek2003]: Hlavacek WS, Faeder JR, Blinov ML, Perelson AS, Goldsten B. 2003. The complexity of complexes in signal transduction. Biotechnology and Bioengineering 84(7):783-94. [Available online](https://onlinelibrary.wiley.com/doi/abs/10.1002/bit.10842)

[^Hlavacek2006]: Hlavacek WS, Faeder JR, Blinov ML, Posner RG, Hucka M, Fontana W. 2006. Rules for modeling signal-transduction systems. Science Signaling 344:re6. [Available online](https://stke.sciencemag.org/content/2006/344/re6.long)

[^ParkinsonLab]: Parkinson Lab website. [website](http://chemotaxis.biology.utah.edu/Parkinson_Lab/projects/ecolichemotaxis/ecolichemotaxis.html)

[^Schwartz14]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 14.1.

[^Schwartz17]: Schwartz R. Biological Modeling and Simulaton: A Survey of Practical Models, Algorithms, and Numerical Methods. Chapter 17.2.

[Next lesson](home_biochem){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


## Extra extra

* The points about SSA, ODE, NFSim need to be fleshed out better. Not sure where they go but I don't think it's in this section. Perhaps in the tutorial unless it is captivating.

BNG supports simulation with Ordinary Differential Equation (ODE) and with Stochastic Simulation Algorithm (SSA, also called Gillespie algorithm). The method is passed in as argument `method=>"ode"` or `method=>"ssa"`.
 - ODE: When simulating a system, we need to define how the system evolves through time. In *continuous* simulation of chemical reactions, the state of the system can be reported given any point in time. The reactions rules specify the rate of change for concentration of the involved species, and they are differential equations. For example, *d[L]/dt=k<sub>dissociate</sub>[L.T] - k<sub>bind</sub>[L][T]*.[^Schwartz14]
 - SSA: When simulating the change of the system through time, we define states of the system. Transition can happen between states that differ by one reaction event. We track the *discrete* amount of each reactants and simulate the system via transition of the states[^Schwartz17]. For example, the state can transit from [#L=100, #T=50, #L.T=0] to [#L=99, #T=49, #L.T=1], with probability determined both by reaction rate *k<sub>bind</sub>* and the the number of ways to choose the L and T molecules.[^Schwartz17] For using SSA, the measurement of abundance of molecules should actually be number of molecule instead of concentration.
