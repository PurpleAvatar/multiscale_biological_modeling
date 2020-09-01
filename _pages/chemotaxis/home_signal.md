---
permalink: /chemotaxis/home_signal
title: "Signaling and Ligand-Receptor Dynamics"
sidebar:
 nav: "chemotaxis"
---

## Cells can detect signals via bonding to receptor proteins

Chemotaxis is one example of many ways in which an organism must be able to perceive a change in its environment and react accordingly. This response is governed by a process called **signal transduction**, in which a cell identifies a stimulus outside the cell and then transmits this stimulus into the cell in order to effect a response.

Although we did not focus on the details at that time, we have already seen an example of signal transduction when we discussed transcription in the [previous module](motifs/transcription). When a certain type of molecule's extracellular concentration increases, **receptor proteins** on the outside of the cell have greater bonding with these molecules and are therefore able to detect changes in molecular concentration. This "signal" is then "transduced" via a series of internal chemical processes that changes a transcription factor into an active state.

In the case of chemotaxis, *E. coli* has receptor proteins that detect attractants such as glucose by binding to and forming a complex with these attractant **ligands**. (The cell also contains receptors to detect repellents, but we will focus primarily on attractants.) In this lesson, we will discuss how the bacterium is able to detect this molecular signal; in the next lesson, we focus on how the bacterium can convert the detected signal into an internal sequence of reactions that lead to a change in movement. See the figure below for a high-level overview of this process.

![image-center](../assets/images/chemotaxis_signal.png){: .align-center}
<figcaption>An overview of the signaling pathway of chemotaxis. The red circles represent attractant ligands(L). When ligands bind to receptors, this signal is transduced via a series of enzymes, and finally influences the rotation direction of a flagellum. We discuss how this response is achieved in a later lesson.</figcaption>


## Modeling ligand-receptor dynamics

Although *E. coli* has different types of surface receptors that can sense a variety of different attractant/repellent ligands in its environment, we will focus on how to model the binding of a single type of receptor to a single type of attractant ligand.

The chemical reactions that we have considered earlier in this course are **irreversible**, meaning they can only proceed in one direction. For example, in the prologue's reaction-diffusion model for [Turing patterns](prologue/animals), we had the reaction *A* + 2*B* → 3*B*, which we conceptualized as two predators eating a prey and reproducing. But we did not have the reverse reaction 3*B* → *A* + 2*B*.

To model ligand-receptor dynamics, we will use a **reversible** reaction that proceeds continuously in both directions at possibly different rates. If a ligand collides with a receptor, then there is some probability that the two molecules will bond into a complex. But at the same time, in any unit of time, there is also some probability that a bound receptor-ligand complex will **dissociate** into two separate molecules. We will discuss the details what makes two molecules more likely to bond in a future module, but for now, we will assert that the more suited a receptor is to a ligand, the higher the bonding rate and the lower the dissociation rate.

Why should ligand-receptor bonding be reversible? First, surface receptors are typically complicated molecules, and it would be costly to an organism if it needed to keep reproducing these molecules rather than sometimes releasing bound ligands. Second, if complexes dissociate, then a brief signal will not be detected by an organism indefinitely; we will say more about how the cell responds to a changing concentration of ligand over time soon.

For now, we will start building a model of ligand-receptor dynamics. We will represent the receptor molecule by *T*, the ligand molecule by *L*, and the bound complex as *TL*. We have the **forward reaction** *T* + *L* → *TL*, which takes place at some rate *k*<sub>bind</sub>, and the **reverse reaction** *TL* → *T* + *L*, which takes place at some rate *k*<sub>dissociate</sub>. If we start with a free floating supply of *T* and *L* molecules, what will happen?

*TL* will initially be formed quickly at the expense of the free-floating *T* and *L* molecules; the reverse reaction will not occur because of the lack of *TL* complexes. As the concentration of *TL* grows and the concentrations of  *T* and *L* decrease, the rate of increase in *TL* will slow. Eventually, the number of *TL* complexes being formed by the forward reaction will balance the number of *TL* complexes being split apart by the reverse reaction. At this point, called a **steady state** or **equilibrium**, the concentration of all particles will stabilize.

## Calculation of steady state concentration in a reversible ligand-receptor reaction

In fact, we can calculate the steady state concentrations of *T* and *L* for our reversible reaction by hand.  Suppose that we begin with initial concentrations of *T* and *L* that are represented by *t*<sub>0</sub> and *l*<sub>0</sub>, respectively. Let [*L*], [*T*], and [*LT*] denote the concentrations of the three molecule types. And assume that the reaction rate constants *k*<sub>bind</sub> and *k*<sub>dissociate</sub> are fixed.

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

This equation may look daunting, but most of its components are constants. In fact, the only unknown is [*LT*], which makes this a quadratic equation, or an equation of the form *a* · *x*<sup>2</sup> + *b* · *x* + *c* = 0 for constants *a*, *b*, and *c* and a single unknown *x*. For this quadratic equation, we have the constants *a* = *k*<sub>bind</sub>, *b* = - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>), and *c* = *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub>.

The "quadratic formula" tells us that the equation *a* · *x*<sup>2</sup> + *b* · *x* + *c* = 0  has solutions given by the following equation:

$$x = \dfrac{-b \pm \sqrt{b^2 - 4 \cdot a \cdot c}}{2 \cdot a}$$

And you thought you'd never need to use the quadratic formula again!

**STOP**: Use the quadratic formula to solve for [*LT*] in our previous equation and find the steady-state concentration of *LT*. How can we use this solution to find the steady-state concentrations of *L* and *T* as well?
{: .notice--primary}

Now that we have reduced the computation of the steady-state concentration of *LT* to the solution of a quadratic equation, let's compute this steady-state concentration for a sample collection of parameters. We will then change the parameters and see how the steady-state concentration changes.

Say that we are given the following parameter values (the units are not important for this toy example):
* *k*<sub>bind</sub> = 2;
* *k*<sub>dissociate</sub> = 5;
* *l*<sub>0</sub> = 50;
* *t*<sub>0</sub> = 50.

Substituting these values into the quadratic equation, we obtain the following:

* *a* = *k*<sub>bind</sub> = 2
* *b* = - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>) = -205
* *c* = *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub> = 5000

That is, we are solving the equation 2 · [*LT*]<sup>2</sup> - 205 · [*LT*] + 5000 = 0. Using the quadratic formula to solve for [*LT*] gives

$$[LT] = \dfrac{205 \pm \sqrt{205^2 - 4 \cdot 2 \cdot 5000}}{2 \cdot 2} = 51.25 \pm 11.25$$.

It would seem that there are *two* solutions: 51.25 + 11.25 = 62.5 and 51.25 - 11.25 = 40. However, because *l*<sub>0</sub> and *t*<sub>0</sub>, the respective initial concentrations of *L* and *T*, are both equal to 50, we cannot have that the steady-state concentration of *LT* is 62.5; as a result, it must be 40.

Now that we know the steady-state concentration of *LT*, we can recover the values of [*L*] and [*T*] too:

[*L*] = *l*<sub>0</sub> - [*LT*] = 10<br>
[*T*] = *t*<sub>0</sub> - [*LT*] = 10

What if the forward reaction were slower? We would imagine that the equilibrium concentration of *LT* would decrease, since the reverse reaction will occur faster than the forward reaction. For example, if we change *k* to 1, then we obtain the following adjusted parameter values:

* *a* = *k*<sub>bind</sub> = 1

* *b* = - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>) = -105

* *c* = *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub> = 2500

In this case, if we solve for [*LT*], we obtain [*LT*] = 36.492; the steady-state concentration has decreased as anticipated.

**STOP**: What do you think will happen to the steady-state concentration of *LT* if the initial concentration (*l*<sub>0</sub>) increases or decreases? What if the dissociation rate (*k*<sub>dissociate</sub>) increases or decreases?  Confirm your prediction by changing the parameters above and solving the quadratic formula for [*LT*].
{: .notice--primary}

Let's use our formula to show how we could determine the steady-state concentration of bound receptor-ligand complexes using values obtained from experiments. We will model an *E. coli* with 7000 receptor molecules in an environment with 10000 ligand molecules. The experimentally determined rate for ligand-receptor binding is *k*<sub>bind</sub> = 0.0146((molecules/µm<sup>3</sup>)<sup>-1</sup>)s<sup>-1</sup>, and the rate for ligand-receptor dissociation is *k*<sub>dissociate</sub> = 35s<sup>-1</sup>.[^Li2004][^Spiro1997][^Stock1991]

* SHUANGER: why would we have different units for the two reaction rates?

For these choices of parameters, we obtain the following constants *a*, *b*, *c* in the quadratic equation:

* *a* = *k*<sub>bind</sub> = 0.0146
* *b* = - (*k*<sub>bind</sub> · *l*<sub>0</sub> + *k*<sub>bind</sub> · *t*<sub>0</sub> + *k*<sub>dissociate</sub>) = -283.2
* *c* = *k*<sub>bind</sub> · *l*<sub>0</sub> · *t*<sub>0</sub> = 1022000

If we solve for [*LT*], we obtain [*LT*] = 4793. Calculate for [*L*] and [*T*]:

[*L*] = *l*<sub>0</sub> - [*LT*] = 5207<br>
[*T*] = *t*<sub>0</sub> - [*LT*] = 2207

## Verifying a theoretical steady-state concentration via stochastic simulation

In the [previous module](motifs), we saw how that we could avoid keeping track of the positions of individual diffusing particles if we assume that these particles are well-mixed, i.e., uniformly distributed throughout their environment. The *E. coli* cell is so small that we will assume that the concentration of any particle in its immediate surroundings is uniform. Therefore, as a proof of concept, let us see if a well-mixed simulation replicates the steady-state concentrations of particles that we just found.

Even though we can calculate steady-state concentrations by hand, we will find a particle-free simulation useful for two reasons. First, this simulation will give us snapshots of the concentrations of particles in the system over multiple time points and allow us to see how quickly the concentrations reach equilibrium. Second, we will soon expand our model of chemotaxis to have many particles and reactions that depend on each other, and direct mathematical analysis of the system like what we have done in the section above will quickly become impossible.  The difficulty at hand is comparable to the famed "*n*-body problem" in physics, where predicting the motions of two celestial objects interacting due to gravity can be done exactly, but there is no known such solution if we add a third body.

Our particle-free model will apply an approach called **Gillespie's Stochastic Simulation Algorithm**, which is often called the **Gillespie algorithm** or just **SSA** for short.

To appreciate how SSA works, say that you own a store and have noticed that on average, there are *k* customers entering your store in a single hour. Let *X* denote the number of customers that enter the store in the next hour; *X* is an example of a **random variable** because it may change based on random chance. If we assume that customers are independent actors and that two customers cannot arrive at the exact same time, then *X* follows a **Poisson distribution**, which means that the probability that exactly *n* customers arrive in the next hour is given by the probability

$$\mathrm{Pr}(n = N) = \dfrac{\lambda^N e^{-\lambda}}{N!}\,.$$

Furthermore, the probability of observing exactly *n* customers in the next *t* hours is given by

$$P(n = N) = \dfrac{(\lambda t)^N e^{-\lambda t}}{N!}\,.$$

* SHUANGER: provide link out to an explanation of where these formulas come from.


We define the states of the system as the discrete amount of reactants, and a transition between one state and another is one molecular event. How likely is a transition to happen is proportional to the rate of that reaction [^Schwartz17].

In our case of ligand-receptor dynamics, we have free ligands *L*, free receptors *T*, which can bind with the rate constant *k*<sub>bind</sub>, and *LT* can dissociate with the rate constant *k*<sub>dissociate</sub>.

At time *t*, there are two reactions that can happen next: *L* + *T* -> *LT* with a rate *k*<sub>bind</sub> · [*L*] · [*T*], and *LT* -> *L* + *T* with a rate *k*<sub>dissociate</sub> · [*LT*]. We define the sum of the two reactions as *R*<sub>tot</sub>. Now we are interested in two questions: when does the next reaction happen, and which reaction is that?

If a customer arrives at time *t*<sub>0</sub>, what is the probability of the next customer arrives after we wait for time *t*<sub>wait</sub> hours? The next customer arrives at *t*<sub>0</sub> + *t*<sub>wait</sub> implies that no one arrives until we've waited for *t*<sub>wait</sub>. The probability of no one arrives during *t*<sub>wait</sub> can be described as $$P(n = 0) = \dfrac{(\lambda t_{wait})^0 e^{-\lambda t_{wait}}}{0!} = e^{-\lambda t_{wait}}$$. Therefore, the probability of the next customer arrives within after *t*<sub>wait</sub> hours is $$P(T \leq t_{wait}) = 1 - e^{-\lambda t_{wait}}$$. To get the *P(T = t<sub>wait</sub>*), we differentiate respect to *t*, and get $$P(T = t_{wait}) = \lambda e^{-\lambda t_{wait}}$$. This distribution is **exponential distribution**, and our wait time t<sub>wait</sub> before the next customer arrives follows an exponential distribution. The expected value (or the average) of the distribution is on average how long does it take for the next customer to arrive, 1/*λ*.

Does this sounds like our question of when the next reaction happen? The process of reactions happening is our Poisson process, the number of reactions happen within a period of time follows the Poisson distribution where reaction rate *R*<sub>tot</sub> indicates the expected number of reactions to happen within the period, and we are interested in the wait time before the next reaction.

The wait time, *δt*, before the next reaction to happen follows an exponential distribution with mean of 1/*R*<sub>tot</sub>. Thus, the time of the system becomes *t* + *δt* after this step. We have the probability of *δt* taking each value now, and we need to get the exact value of *δt*. This process is similar to rolling a dice, and we have a dice with infinite number of sides, and the probability of getting each side is not equal; or, plotting cutting a piece of paper to replicate the probability distribution function and throwing darts onto that piece of paper. In simulations, **sampling** is the key to replicate the stochasticity in nature, and can conveniently done by computer programs.

Our second question was to decide which reaction happen next. This is similar to tossing a biased coin; the faster the reaction rate, the more likely the reaction to happen.

The probability of each reaction to happen is *P(reaction)* = *R*<sub>reaction</sub> / *R*<sub>tot</sub>

Therefore, *P(L + T -> LT)* = *k*<sub>bind</sub> · [*L*] · [*T*] / *R*<sub>tot</sub>

*P(LT -> L + T)* = *k*<sub>dissociate</sub> · [*LT*] / *R*<sub>tot</sub>

This process is visualized below.

![image-center](../assets/images/chemotaxis_visualizessa.png){: .align-center}
<figcaption>Visualization of one transition for SSA. Red circles represent ligands(L). Orange Pac-man shape represent receptors. The wait time for a reaction to happen at time <i>t</i>, <i>δt</i> is drawn from an exponential distribution with mean 1/<i>R</i><sub>tot</sub>. The probability of dissociation (upper) or binding (lower) is determined by the rate of the reaction.</figcaption>

The following tutorial uses [BioNetGen](http://bionetgen.org/), which we will use throughout this module to build particle-free simulations of chemotaxis. We start by building a model to determine the equilibrium of a reversible reaction involving ligands and receptors.

[Visit tutorial](tutorial_lr){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Does a simulation confirm our steady-state calculations?

Here we've shown that using BNG and calculating by hand reach the same conclusion for bimolecular reactions.

From the BNG simulation, we can observe that *L* and *T* drop quickly while *LT* increases quickly at the begining of the simulation, and then reach steady state concentrations. The steady state concentrations match our calculations by hand.

![image-center](../assets/images/chemotaxis_tutorial4_ssa.png){: .align-center}
<figcaption>Concentration plot for ligand-receptor dynamics with SSA simulation. The concentrations reach a steady state at the end of the simulation.</figcaption>

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

[^Li2004]: Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^Stock1991]: Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^Spiro1997]: Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).

[Next lesson](home_biochem){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


## Extra extra

* The points about SSA, ODE, NFSim need to be fleshed out better. Not sure where they go but I don't think it's in this section. Perhaps in the tutorial unless it is captivating.

BNG supports simulation with Ordinary Differential Equation (ODE) and with Stochastic Simulation Algorithm (SSA, also called Gillespie algorithm). The method is passed in as argument `method=>"ode"` or `method=>"ssa"`.
 - ODE: When simulating a system, we need to define how the system evolves through time. In *continuous* simulation of chemical reactions, the state of the system can be reported given any point in time. The reactions rules specify the rate of change for concentration of the involved species, and they are differential equations. For example, *d[L]/dt=k<sub>dissociate</sub>[L.T] - k<sub>bind</sub>[L][T]*.[^Schwartz14]
 - SSA: When simulating the change of the system through time, we define states of the system. Transition can happen between states that differ by one reaction event. We track the *discrete* amount of each reactants and simulate the system via transition of the states[^Schwartz17]. For example, the state can transit from [#L=100, #T=50, #L.T=0] to [#L=99, #T=49, #L.T=1], with probability determined both by reaction rate *k<sub>bind</sub>* and the the number of ways to choose the L and T molecules.[^Schwartz17] For using SSA, the measurement of abundance of molecules should actually be number of molecule instead of concentration.

Removew the ODE results
![image-center](../assets/images/chemotaxis_tutorial4.png){: .align-center}
<figcaption>Concentration plot for ligand-receptor dynamics with ODE simulation. The concentrations reach a steady state at the end of the simulation. </figcaption>
