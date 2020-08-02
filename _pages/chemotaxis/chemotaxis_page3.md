---
permalink: /chemotaxis/tutorial_adap
title: "Adaptation"
sidebar: 
 nav: "chemotaxis"
---

In this page, we will:
 - Add adaptation mechanisms
 - Learn compartmentalization rules for BNG and add to our model
 - Include cellular concentrations and reaction rates for our system
 - Explore the behavior of CheY

### Adding Adaptation Mechanisms

If one *E. coli* is in a well-mixed glucose solution with a concentration of *A*, and another is in a well-mixed glucose with a concentration of *10A*, should they have the same tumbling frequency? If the second one tumbles less, it will have a harder time to move towards a even higher concentration. So now let's add methylation states to model how *E. coli* can adapt to a higher attractant concentrations and bring back the tumbling frequency.

Our model will be based on the [model](https://www.pnas.org/content/94/14/7263) by Spiro et al.[^1]

The methylation states of the receptors store the *past* ligand concentrations. If we have a high level ligand-receptor binding, and that is consistent with the methylation states, then the cell doesn't need to decrease its tumbling frequency because no gradient is present. This is achieved by using higher methylation states to reflect higher past ligand concentration, and higher rates of autophosphorylation for higher methylation states. The increased phosphorylation due to higher methylation states can compensate for the low phosphorylation due to high levels of ligand binding. 

Let's first add methylation states, low (A), medium (B), high (C), for the ternary complex. Also add a component `r` for later introduction of CheR. Update `T` to be `T(l,r,Meth~A~B~C,Phos~U~P)`.

Then we change the receptor autophosphorylation rules to reflect what we've just discussed. Since we are defining a lot of reactions, it might be helpful to give the reaction rate parameters more meaningful names.

	#Receptor complex (specifically CheA) autophosphorylation
	#Rate dependent on methylation and binding states
	#Also on free vs. bound with ligand

	TaUnboundP: T(l,Meth~A,Phos~U) -> T(l,Meth~A,Phos~P) k_TaUnbound_phos
	TbUnboundP: T(l,Meth~B,Phos~U) -> T(l,Meth~B,Phos~P) k_TaUnbound_phos*1.1
	TcUnboundP: T(l,Meth~C,Phos~U) -> T(l,Meth~C,Phos~P) k_TaUnbound_phos*2.8
	TaLigandP: L(t!1).T(l!1,Meth~A,Phos~U) -> L(t!1).T(l!1,Meth~A,Phos~P) 0
	TbLigandP: L(t!1).T(l!1,Meth~B,Phos~U) -> L(t!1).T(l!1,Meth~B,Phos~P) k_TaUnbound_phos*0.8
	TcLigandP: L(t!1).T(l!1,Meth~C,Phos~U) -> L(t!1).T(l!1,Meth~C,Phos~P) k_TaUnbound_phos*1.6

The methylation states of the receptor complexes are modified by CheR and CheB. CheR binds to receptor complexes and methylates them; the rate of methylation is higher for ligand-bound receptors. CheB is phosphorylated by CheA in the receptor complex, and CheB-P then demethylates receptor complexes; the rate of demethylation is independent of ligand-binding. Therefore more ligand binding leads to higher methylation states. The rate of entering an intermediate methylation state is faster, enabling fast adaptation. 

Add `CheB(Phos~U~P)` and `CheR(t)` to the `molecule types` section. And add reactions we just discussed to `reaction rules`.

	#CheR binds to and methylates receptor complex
	#Rate dependent on methylation states and ligand binding
	TRBind: T(r) + CheR(t) <-> T(r!2).CheR(t!2) k_TR_bind, 1
	TaRUnboundMeth: T(r!2,l,Meth~A).CheR(t!2) -> T(r,l,Meth~B) + CheR(t) k_TaR_meth
	TbRUnboundMeth: T(r!2,l,Meth~B).CheR(t!2) -> T(r,l,Meth~C) + CheR(t) k_TaR_meth*0.1
	TaRLigandMeth: T(r!2,l!1,Meth~A).L(t!1).CheR(t!2) -> T(r,l!1,Meth~B).L(t!1) + CheR(t) k_TaR_meth*30
	TbRLigandMeth: T(r!2,l!1,Meth~B).L(t!1).CheR(t!2) -> T(r,l!1,Meth~C).L(t!1) + CheR(t) k_TaR_meth*3
	
	#CheB is phosphorylated by receptor complex, and autodephosphorylates
	CheBphos: T(Phos~P) + CheB(Phos~U) -> T(Phos~U) + CheB(Phos~P) k_B_phos
	CheBdephos: CheB(Phos~P) -> CheB(Phos~U) k_B_dephos
	
	#CheB demethylates receptor complex
	#Rate dependent on methyaltion states
	TbDemeth: T(Meth~B) + CheB(Phos~P) -> T(Meth~A) + CheB(Phos~P) k_Tb_demeth
	TcDemeth: T(Meth~C) + CheB(Phos~P) -> T(Meth~B) + CheB(Phos~P) k_Tc_demeth

Now we have a complete set of reaction rules. For convenience, give all reaction rates some meaningful names.

	begin reaction rules
		LigandReceptor: L(t) + T(l) <-> L(t!1).T(l!1) k_lr_bind, k_lr_dis
		
		#Receptor complex (specifically CheA) autophosphorylation
		#Rate dependent on methylation and binding states
		#Also on free vs. bound with ligand
		TaUnboundP: T(l,Meth~A,Phos~U) -> T(l,Meth~A,Phos~P) k_TaUnbound_phos
		TbUnboundP: T(l,Meth~B,Phos~U) -> T(l,Meth~B,Phos~P) k_TaUnbound_phos*1.1
		TcUnboundP: T(l,Meth~C,Phos~U) -> T(l,Meth~C,Phos~P) k_TaUnbound_phos*2.8
		TaLigandP: L(t!1).T(l!1,Meth~A,Phos~U) -> L(t!1).T(l!1,Meth~A,Phos~P) 0
		TbLigandP: L(t!1).T(l!1,Meth~B,Phos~U) -> L(t!1).T(l!1,Meth~B,Phos~P) k_TaUnbound_phos*0.8
		TcLigandP: L(t!1).T(l!1,Meth~C,Phos~U) -> L(t!1).T(l!1,Meth~C,Phos~P) k_TaUnbound_phos*1.6
		
		#CheY phosphorylation by T and dephosphorylation by CheZ
		YPhos: T(Phos~P) + CheY(Phos~U) -> T(Phos~U) + CheY(Phos~P) k_Y_phos
		YDephos: CheZ() + CheY(Phos~P) -> CheZ() + CheY(Phos~U) k_Y_dephos
		
		#CheR binds to and methylates receptor complex
		#Rate dependent on methylation states and ligand binding
		TRBind: T(r) + CheR(t) <-> T(r!2).CheR(t!2) k_TR_bind, 1
		TaRUnboundMeth: T(r!2,l,Meth~A).CheR(t!2) -> T(r,l,Meth~B) + CheR(t) k_TaR_meth
		TbRUnboundMeth: T(r!2,l,Meth~B).CheR(t!2) -> T(r,l,Meth~C) + CheR(t) k_TaR_meth*0.1
		TaRLigandMeth: T(r!2,l!1,Meth~A).L(t!1).CheR(t!2) -> T(r,l!1,Meth~B).L(t!1) + CheR(t) k_TaR_meth*30
		TbRLigandMeth: T(r!2,l!1,Meth~B).L(t!1).CheR(t!2) -> T(r,l!1,Meth~C).L(t!1) + CheR(t) k_TaR_meth*3
		
		#CheB is phosphorylated by receptor complex, and autodephosphorylates
		CheBphos: T(Phos~P) + CheB(Phos~U) -> T(Phos~U) + CheB(Phos~P) k_B_phos
		CheBdephos: CheB(Phos~P) -> CheB(Phos~U) k_B_dephos
		
		#CheB demethylates receptor complex
		#Rate dependent on methyaltion states
		TbDemeth: T(Meth~B) + CheB(Phos~P) -> T(Meth~A) + CheB(Phos~P) k_Tb_demeth
		TcDemeth: T(Meth~C) + CheB(Phos~P) -> T(Meth~B) + CheB(Phos~P) k_Tc_demeth
		
	end reaction rules


### Adding Compartments

In biological systems, plasma membrane separates molecules inside of the cell from the environment. In our chemotaxis system, ligand are outside of the cell, receptors and flagellar proteins are on the membrane, and CheY, CheR, CheB, CheZ are inside the cell. Therefore we will also add this compartmentalization into our model.

We will define extra-cellular spaces, plasma membrane, and cytoplasm. Here, each row indicates 1) name of the compartment, 2) dimension (2D or 3D), 3) surface area or volumn of the compartment, 4) the name of the parent compartment. More information on compartmentalization can be found page 54-55 [here](http://www.lehman.edu/academics/cmacs/documents/RuleBasedPrimer-2011.pdf).

	begin compartments
		EC  3  100       #um^3
		PM  2  1   EC    #um^2
		CP  3  1   PM    #um^3
	end compartments


### Specifying concentrations and reaction rates

We need to add the compartmentalization information in the `seed species`. Also update the initial concentrations of molecules at different states. The distribution of molecules are each state is very difficult to experimentally verify. The distribution provided here approximates equilibrium concentrations in our simulation, and they are within a biologically reasonable range.[^2]

	begin seed species
		@EC:L(t) L0
		@PM:T(l,r,Meth~A,Phos~U) T0*0.84*0.9
		@PM:T(l,r,Meth~B,Phos~U) T0*0.15*0.9
		@PM:T(l,r,Meth~C,Phos~U) T0*0.01*0.9
		@PM:T(l,r,Meth~A,Phos~P) T0*0.84*0.1
		@PM:T(l,r,Meth~B,Phos~P) T0*0.15*0.1
		@PM:T(l,r,Meth~C,Phos~P) T0*0.01*0.1
		@CP:CheY(Phos~U) CheY0*0.71
		@CP:CheY(Phos~P) CheY0*0.29
		@CP:CheZ() CheZ0
		@CP:CheB(Phos~U) CheB0*0.62
		@CP:CheB(Phos~P) CheB0*0.38
		@CP:CheR(t) CheR0
	end seed species

Specify all the molecules types you want to observe for in the `observable` section.

	begin observables
		Molecules BoundLigand L(t!1).T(l!1)
		Molecules ActiveCheY CheY(Phos~P)
		Molecules TA T(Meth~A)
		Molecules TB T(Meth~B)
		Molecules TC T(Meth~C)
		Molecules ActiveCheB CheB(Phos~P)
	end observables

And the last thing to be done is to assign values to the parameters. Let's start with no ligand is added to the system. We assign the initial number for each molecule and reaction rates by first deciding a reasonable range based on *in vivo* stoichiometry [^1][^3][^4] and then tuning to fit the model. 

From the experimental results, we have the number of each molecules in each cell, but our reaction rates are in the unit of M/s, so we need to do some unit conversion. The volume of *E. coli* is approximately 1um^3, so our molecule counts are of unit num_molecule/um^3. One mole of molecule is approximately 6.02 * 10^23 molecules (Avogadro's number), so the unit M is approximately 6.02 * 10^23 molecules/L, which is about 6.02 * 10^8 molecules/um^3. We record this as NaV2. For bimolecular reactions, the rate constant should have unit (M^-1)(s^-1), and we devide NaV2 to convert to ((molecules/um^3)^-1)(s^-1). For monomolecular reactions, the rate constant have unit (s^-1), so no unit conversion is required.

	begin parameters
		NaV2 6.02e8   #Unit conversion to cellular concentration M/L -> #/um^3
		miu 1e-6
		
		L0 0             #number of molecules/cell
		T0 7000          #number of molecules/cell
		CheY0 20000      #number of molecules/cell
		CheZ0 6000       #number of molecules/cell
		CheR0 120        #number of molecules/cell
		CheB0 250        #number of molecules/cell
		
		k_lr_bind 8.8e6/NaV2   #ligand-receptor binding
		k_lr_dis 35            #ligand-receptor dissociation
		
		k_TaUnbound_phos 7.5   #receptor complex autophosphorylation
		
		k_Y_phos 3.8e6/NaV2    #receptor complex phosphorylates Y
		k_Y_dephos 8.6e5/NaV2  #Z dephosphoryaltes Y
		
		k_TR_bind  2e7/NaV2    #Receptor-CheR binding
		k_TR_dis   1           #Receptor-CheR dissociation
		k_TaR_meth 0.08        #CheR methylates receptor complex
		
		k_B_phos 1e5/NaV2      #CheB phosphorylation by receptor complex
		k_B_dephos 0.17        #CheB autodephosphorylation
		
		k_Tb_demeth 5e4/NaV2   #CheB demethylates receptor complex
		k_Tc_demeth 2e4/NaV2   #CheB demethylates receptor complex
	end parameters

### The complete code

	begin model

	begin molecule types
		L(t)
		T(l,r,Meth~A~B~C,Phos~U~P)
		CheY(Phos~U~P)
		CheZ()
		CheB(Phos~U~P)
		CheR(t)
	end molecule types

	begin parameters
		NaV2 6.02e8   #Unit conversion to cellular concentration M/L -> #/um^3
		miu 1e-6
		
		L0 0
		T0 7000
		CheY0 20000
		CheZ0 6000
		CheR0 120
		CheB0 250
		
		k_lr_bind 8.8e6/NaV2   #ligand-receptor binding
		k_lr_dis 35            #ligand-receptor dissociation
		
		k_TaUnbound_phos 7.5   #receptor complex autophosphorylation
		
		k_Y_phos 3.8e6/NaV2    #receptor complex phosphorylates Y
		k_Y_dephos 8.6e5/NaV2  #Z dephosphoryaltes Y
		
		k_TR_bind 0.2*miu*NaV2 #Receptor-CheR binding
		k_TaR_meth 0.08        #CheR methylates receptor complex
		
		k_B_phos 1e5/NaV2      #CheB phosphorylation by receptor complex
		k_B_dephos 0.17        #CheB autodephosphorylation
		
		k_Tb_demeth 5e4/NaV2   #CheB demethylates receptor complex
		k_Tc_demeth 2e4/NaV2   #CheB demethylates receptor complex
	end parameters

	begin compartments
	  EC  3  100       #um^3
	  PM  2  1   EC    #um^2
	  CP  3  1   PM    #um^3
	end compartments

	begin reaction rules
		LigandReceptor: L(t) + T(l) <-> L(t!1).T(l!1) k_lr_bind, k_lr_dis
		
		#Receptor complex (specifically CheA) autophosphorylation
		#Rate dependent on methylation and binding states
		#Also on free vs. bound with ligand
		TaUnboundP: T(l,Meth~A,Phos~U) -> T(l,Meth~A,Phos~P) k_TaUnbound_phos
		TbUnboundP: T(l,Meth~B,Phos~U) -> T(l,Meth~B,Phos~P) k_TaUnbound_phos*1.1
		TcUnboundP: T(l,Meth~C,Phos~U) -> T(l,Meth~C,Phos~P) k_TaUnbound_phos*2.8
		TaLigandP: L(t!1).T(l!1,Meth~A,Phos~U) -> L(t!1).T(l!1,Meth~A,Phos~P) 0
		TbLigandP: L(t!1).T(l!1,Meth~B,Phos~U) -> L(t!1).T(l!1,Meth~B,Phos~P) k_TaUnbound_phos*0.8
		TcLigandP: L(t!1).T(l!1,Meth~C,Phos~U) -> L(t!1).T(l!1,Meth~C,Phos~P) k_TaUnbound_phos*1.6
		
		#CheY phosphorylation by T and dephosphorylation by CheZ
		YPhos: T(Phos~P) + CheY(Phos~U) -> T(Phos~U) + CheY(Phos~P) k_Y_phos
		YDephos: CheZ() + CheY(Phos~P) -> CheZ() + CheY(Phos~U) k_Y_dephos
		
		#CheR binds to and methylates receptor complex
		#Rate dependent on methylation states and ligand binding
		TRBind: T(r) + CheR(t) <-> T(r!2).CheR(t!2) k_TR_bind, k_TR_dis
		TaRUnboundMeth: T(r!2,l,Meth~A).CheR(t!2) -> T(r,l,Meth~B) + CheR(t) k_TaR_meth
		TbRUnboundMeth: T(r!2,l,Meth~B).CheR(t!2) -> T(r,l,Meth~C) + CheR(t) k_TaR_meth*0.1
		TaRLigandMeth: T(r!2,l!1,Meth~A).L(t!1).CheR(t!2) -> T(r,l!1,Meth~B).L(t!1) + CheR(t) k_TaR_meth*30
		TbRLigandMeth: T(r!2,l!1,Meth~B).L(t!1).CheR(t!2) -> T(r,l!1,Meth~C).L(t!1) + CheR(t) k_TaR_meth*3
		
		#CheB is phosphorylated by receptor complex, and autodephosphorylates
		CheBphos: T(Phos~P) + CheB(Phos~U) -> T(Phos~U) + CheB(Phos~P) k_B_phos
		CheBdephos: CheB(Phos~P) -> CheB(Phos~U) k_B_dephos
		
		#CheB demethylates receptor complex
		#Rate dependent on methyaltion states
		TbDemeth: T(Meth~B) + CheB(Phos~P) -> T(Meth~A) + CheB(Phos~P) k_Tb_demeth
		TcDemeth: T(Meth~C) + CheB(Phos~P) -> T(Meth~B) + CheB(Phos~P) k_Tc_demeth
		
	end reaction rules

	begin seed species
		@EC:L(t) L0
		@PM:T(l,r,Meth~A,Phos~U) T0*0.84*0.9
		@PM:T(l,r,Meth~B,Phos~U) T0*0.15*0.9
		@PM:T(l,r,Meth~C,Phos~U) T0*0.01*0.9
		@PM:T(l,r,Meth~A,Phos~P) T0*0.84*0.1
		@PM:T(l,r,Meth~B,Phos~P) T0*0.15*0.1
		@PM:T(l,r,Meth~C,Phos~P) T0*0.01*0.1
		@CP:CheY(Phos~U) CheY0*0.71
		@CP:CheY(Phos~P) CheY0*0.29
		@CP:CheZ() CheZ0
		@CP:CheB(Phos~U) CheB0*0.62
		@CP:CheB(Phos~P) CheB0*0.38
		@CP:CheR(t) CheR0
	end seed species

	begin observables
		Molecules BoundLigand L(t!1).T(l!1)
		Molecules ActiveCheY CheY(Phos~P)
		Molecules TA T(Meth~A)
		Molecules TB T(Meth~B)
		Molecules TC T(Meth~C)
		Molecules ActiveCheB CheB(Phos~P)
	end observables

	end model

	generate_network({overwrite=>1})
	simulate({method=>"ode", t_end=>1000, n_steps=>1000})


### Adaptation: CheY returns to equilibrium

Fantastic, we have the model now.

Now run the simulation (please change `t_end` and `n_steps` to 1000). You should be able to observe none of the observable change in concentration with no ligand present.

![image-center](../assets/images/chemotaxis_tutorial_oneadd0.png){: .align-center}

Try with higher concentrations (L0 = 1e4, 1e5, 1e6, 1e7, 1e8), highlight the line showing CheY-P, we could see a drop in CheY-P at the start of the simulation, and then returns to the original concentration. We could also see how the methylation states changed. You can also simulate the first 10 seconds of the simulation to observe the minumum of CheY-P occured within the first second.

L0 = 1e4.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e4.png){: .align-center}
L0 = 1e5.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e5.png){: .align-center}
L0 = 1e6.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e6.png){: .align-center}
L0 = 1e7.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e7.png){: .align-center}
L0 = 1e8.
![image-center](../assets/images/chemotaxis_tutorial_oneadd1e8.png){: .align-center}

We can see that the higher the concentration, the lower the valley becomes. But this limited to a range of concentrations - going over a concentration where all receptors can already saturate instantly can't lead to more response; and a very low concentration won't initiate a response. Our results are also consistent with other simulations[^2] and experimental observations[^5][^6]. 

We will be simulating exponential gradients in the next page!

[^1] Spiro PA, Parkinson JS, and Othmer H. 1997. A model of excitation and adaptation in bacterial chemotaxis. Biochemistry 94:7263-7268. [Available online](https://www.pnas.org/content/94/14/7263).

[^2] Bray D, Bourret RB, Simon MI. 1993. Computer simulation of phosphorylation cascade controlling bacterial chemotaxis. Molecular Biology of the Cell. [Available online](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC300951/)

[^3] Li M, Hazelbauer GL. 2004. Cellular stoichimetry of the components of the chemotaxis signaling complex. Journal of Bacteriology. [Available online](https://jb.asm.org/content/186/12/3687)

[^4] Stock J, Lukat GS. 1991. Intracellular signal transduction networks. Annual Review of Biophysics and Biophysical Chemistry. [Available online](https://www.annualreviews.org/doi/abs/10.1146/annurev.bb.20.060191.000545)

[^5] Shimizu TS, Delalez N, Pichler K, and Berg HC. 2005. Monitoring bacterial chemotaxis by using bioluminescence resonance energy transfer: absence of feedback from the flagellar motors. PNAS. [Available online](https://www.pnas.org/content/103/7/2093/)

[^6] Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)


[Previous](tutorial_phos){: .btn .btn--primary .btn--x-large} [Next Page](tutorial_gradient){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}




