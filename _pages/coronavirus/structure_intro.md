---
permalink: /coronavirus/structure_intro
title: Introduction to Protein Structure Prediction
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---
## Protein Structure Basics

Proteins are one of the most important groups of macromolecules in living organisms, contributing to essentially all functions within them. Recall that in the *Introduction to Transcription* section of the Motifs module, we were introduced to the central dogma of molecular biology: DNA to RNA to protein. We saw that after the translation step of mRNA to a polypeptide that will typically undergo folding to obtain a 3D structure.

Protein structure can be separated into four different levels of description. The most basic description, the primary structure, refers the specific amino acid sequence of the polypeptide chain. In the first figure below, the general shape of the amino acid is shown: a central alpha-Carbon, a carboxyl group, an amino group, and finally one of 20 side-groups that differentiate the amino acids. Each amino acid is linked to the next by a peptide bond, and it is this connection and alpha-Carbon that make up the protein backbone, as shown in the second figure. The side groups are responsible for giving the amino acid its chemical properties.

<img src="../_pages/coronavirus/files/AminoAcid.png">

<img src="../_pages/coronavirus/files/Backbone.png">

The secondary structure describes the highly regular substructures in the protein. The two main substructures, shown in the figure below, are alpha-helices (left) and beta-sheets (right). Essentially, they are the 3D structures of local segments within the protein and are formed as an intermediate before the overall protein structure are formed.

<img src="../_pages/coronavirus/files/SecondaryStructure.png">

The tertiary structure describes the overall 3D shape of the protein that results from how the peptide chain folds together. The interactions between the side groups are what dictates how the protein folds (e.g. H-bonds, disulfide bridges, hydrophobic/hydrophilic interactions, electrostatic interactions, and van der Waals interactions).

Finally, some proteins have a quaternary structure, which describes the protein’s interaction with other copies of itself to form a single functional unit, or a multimer. 

Now that we have a pretty good understanding of protein structure, we need to explain why the 3D structure is so important.

## Protein Shape is Key

The shape of the protein, or tertiary structure, is essential when it comes to function and interactions with other proteins or ligands. There are a few models for describing this interaction, the simplest being Emil Fischer’s classic “lock and key” model for the enzyme and substrate. This model was created as an analogy to enzyme specificity, or the ability of enzymes to interact only with its target substrate, where the enzyme is the “lock” and the substrate is the “key”. If the substrate does not fit into the active site of the enzyme, no biochemical process will happen; just like if the key does not fit the lock, then nothing happens. However, proteins are not rigid, but rather show conformational flexibility. As a result, Daniel Koshland introduced a modified model called the “induced fit” model. Rather than a rigid lock, think of it as a pin tumbler lock. The notches on the key causes the pins of the lock to shift until the correct configuration is reached and the lock opens. Similarly, the interaction site of proteins does not 100% match the shape of their target. Instead, the target will align and interact with a portion of the site and induce conformational change to the appropriate shape for biochemical processes to start. Nonetheless, if the shape of the key completely different, it will not even be able to interact with the lock in the first place.

For molecules to react with each other, not only do they have to physically collide with one another, it also must be in the correct orientation. However, this does not even guarantee that the reaction will occur. It is possible for the molecule to disassociate before anything even happens. A common theme in chemistry is that reactions do not typically proceed to completion. Many intermediate steps are reversible, just like the reversible reactions we see in the chemotaxis model. The same thing happens for protein interactions. Any two proteins have the probability of *interacting*, but if two proteins don’t fit together well enough, then the probability of two associated proteins disassociating in a given time step is much higher than if the proteins interact.

The world is ruled by probability again!

## The Shape is Not Unique

Remember back to the four levels of protein structure. We stated that the overall 3D structure (tertiary structure) of the protein is dictated by the interactions of the side chains. Even when we unfold, or denature, a protein, it will eventually fold back into essentially the same shape because of these interactions. Small perturbations in the sequence may have dramatic effects on the overall structure and even render the protein useless. You may think that every structure has its own specific sequence of amino acids (primary structure), but this is far from the truth. Although there are twenty amino acids, they are often grouped together by having similar chemical properties (i.e. polarity and charge). As a result, two very different sequences can have the exact same function and extremely similar structures.

As an example, let’s compare the sequences and structures of hemoglobin subunit alpha from Humans (*Homo sapiens*; PDB: <a href="https://www.rcsb.org/structure/1SI4" target="_blank">1si4</a>) Shortfin Mako Sharks (*Isurus oxyrinchus* ; PDB: <a href="https://www.rcsb.org/structure/3mkb" target="_blank">3mkb</a>) and emus (*Dromaius novaehollandia*; PDB: <a href="https://www.rcsb.org/structure/3wtg" target="_blank">3wtg</a>). From the figures below, we can see that the proteins are markedly different in terms of primary structure. Nonetheless, the 3D structures are essentially the same. (Sequence identity is the measurement of how similar two different sequences are by calculating the number of positions that share the same character.)

<img src="../_pages/coronavirus/files/SequenceStructureExample.png">

## Methods of Finding Protein Structure

From everything we discussed thus far, it should be easy to see why such a large part of molecular biology is dedicated to analyzing protein tertiary structure. Even when studying an unknown protein, we can predict its function just by knowing what it looks like. There are several methods used to accurately determine the protein structure, such as X-ray crystallography, NMR spectroscopy, and electron microscopy. 

X-ray crystallography (sometimes referred to as macromolecular crystallography, or MX) works by first crystallizing the protein and then subjecting it to an intense x-ray beam. The protein will diffract the beam and create patters that describe the electron distribution in the protein. By creating a map of the electron density, it can be analyzed to determine the position of each atom. Thus, x-ray crystallography can determine the protein structure with extreme precision. Unfortunately, there are many drawbacks. First, the process of crystallization is complex, limiting the types of protein that can be analyzed this way. Second, flexible proteins are difficult to study since x-ray crystallography relies on having large amounts of molecules that need to be aligned in the exact same orientation. Third, x-ray crystallography is very expensive, with services charging around $2000 dollars for a single sample. 

For NMR spectroscopy, proteins are placed in a magnetic field and probed with radio waves. The set of resonance can then be analyzed to produce a list of atomic nuclei that are in close proximity and to characterize the local conformation of the atoms. One of the benefits of this method is that the protein can be studied in solution, offering information of the protein in a more realistic environment. NMR spectroscopy can cost up to $500 dollars and are limited to small or medium proteins. 

Electron microscopy (3DEM) directly images the molecule by using a system of electron lenses. Producing 3D images requires imaging thousands of different particles that are preserved in non-crystalline ice (cryo-EM). Improvements in 3DEM have allowed resolution of the images to improve drastically and in some cases, reaching the resolution levels of NMR spectroscopy. However, because electron microscopes are extremely complicated machinery, purchasing one may cost anywhere between $100,000 to the most expensive $27 million (located in Lawrence Berkeley National Lab).

## Storing Protein Structure

* After experimentally determining the 3D protein structure, the structure is typically uploaded into the PDB as a .pdb file. This file is extremely dense as it holds all the details about the protein, from the very basic primary structure of the protein all the way to the position of every single atom. The simplest way to think about how the entire protein is stored is to first represent atoms as points on a 3D plane with each atom having its 3D orthogonal coordinates (X,Y,Z) in the unit of angstroms. This is the atomic coordinates of the protein. A simplified view of the atomic coordinates section is shown in the first figure below. 

*Because the structure of the 20 amino acids are well studied, we know which atoms are connected within each residue. The atomic bonds that link amino acids in sequence are easy to deduce from the primary structure of the protein. However, the angles of these connections also need to be explicit to describe the 3D structures. These angles are referred to as peptide torsion angles, shown in the second figure below. The two bonds connecting the alpha carbon of an amino acid are able rotate, allowing a peptide chain to be able to fold into many different possible conformations. Phi (φ) refers to the bond angle connecting to the amino group and psi (ψ) refers to the bond angle connecting to the carboxyl group. The specific set of phi and psi angles of the protein helps describe the structure of the protein. Omega (ω) describes the bond angle of the peptide bond between two amino acids, but is almost always locked at 180°. There exists connections between residues that cannot be infered from the primary structure (e.g. disulfide bonds) which are also described within the file. This is just scratching the tip of the iceberg of the information required to represent a protein structure. For more information, check out the <a href="http://www.wwpdb.org/documentation/file-format" target="_blank">official PDB documentation</a>.

<img src="../_pages/coronavirus/files/simplifiedPDB.png">

<img src="../_pages/coronavirus/files/psiphi.png">

## The Problem with the Common Methods

Protein structures that have been determined are typically stored in the Protein Data Bank (PDB) and is constantly growing larger and larger. As of 1 April 2020, there are a total of 162,269 entries on the PDB, but is this really a large number?

<img src="../_pages/coronavirus/files/PDBGraph.png">

Let’s take a look at the human proteome. In a human proteome study published in 2016, it was estimated that between 0.62 to 6.13 million protein species can exist in humans. Now consider that the natural world is estimated to have 8.7 million species. 162,269 number of protein structures now looks like an incredibly small number, even when protein conservation between species is taken into account. Given the current speed of new entries, we would never be able to record this many protein structures. Another problem is these methods of structure determination they need the actual physical proteins themselves. In microbiology, it is estimated that of all bacterial life, less than 2% of bacteria can be cultured in the lab [^1]. Rather than culturing and isolating bacteria, we can directly study DNA (metagenomics), RNA (metatranscriptomics), and proteins (metaproteomics) found directly in the environment or surrounding biomasses. However, we cannot just hope to find all the different proteins by chance. So, what can we do? One potential strategy is to create algorithms for predicting protein structure directly from the protein sequence.

* Levinthal’s Paradox. Large number of degrees of freedom in a polypeptide chain. Given a chain with 100 residues, there will be 99 peptide bonds, resulting in 198 phi and psi bond angles. If each bond has three stable conformations, then there are a maximum of $$ 3^[198] $$ different possible conformations. Will take longer than the age of the universe to sample all conformation to find the correct native form. Paradox is that most natural protein folding occurs spontaneously, typically within the timescale of milliseconds. The fastest within a couple of microseconds [^1].
  * Local residues form stable interactions an act as nucleation points (protein folding intermediates and partial-folded transition states), facilitation folding speed.
  * Proposed funnel-like energy landscapes (not really the case, the energy landscape is more like a caldera).
  * Main point: need A LOT of computing 
  * Nature has a magic algorithm for protein folding. Can we find it?
  
## Protein Structure Prediction

The first whole genome sequence of SARS-CoV-2 isolate *Wuhan-Hu-1* was released on 10 January 2020 by Wu, F. et. al., and is available in GenBank along with the genome annotations [^2][^3]. Perhaps due to the SARS 2003 outbreak, many different types of coronaviruses have been sequenced and studied. Upon sequence comparison, SARS-CoV-2 was found to be related to several coronaviruses isolated from bats and distantly related to SARS-CoV-1. In fact, SARS-CoV-2 has a sequence identity of around 96% with bat coronavirus RaTG13, leading to the hypothesis that the virus originated from bats, which is further supported by the fact that bats are natural reservoir hosts of SARS-related coronaviruses.


<img src="../_pages/coronavirus/files/SARSCoV2Annotation.png">

The question is whether we can predict the structure of the Spike protein directly form the sequence of its gene in DNA?

The point of this question is that we can compare our algorithm for structure prediction against known 3-D structures (SARS1 before the SARS2 3-D structure was known experimentally, and both viruses afterward). Researchers would do this to see how good our algorithm is at reproducing a known structure as a proof of concept for the approach when we don’t have funds for X-ray crystallography but want a reliable representation of a newly sequenced protein’s structure.

Unfortunately, protein structure prediction from sequence is a *extremely difficult* problem. In fact, we would need a very good understanding of all the small interactions that occur between atoms during protein folding, including bonding energy, electrostatic interactions, van der Waals interactions, thermodynamics; all which are subject to alterations depending on the environment. Regardless of its difficulty, protein structure prediction is a very important problem to solve given its potential for many, many applications. Perhaps one of the most important applications is in structure-based drug design. When developing a drug, knowing its 3D structure not only helps us understand how the drug will interact with the target or potential off-targets, it will also help us test more potential drug candidates, refine and create better drugs, and ultimately speed the process up. The Soviets founded a research institute to solve this problem once and for all in the 1960s. The Soviet Union ended 3 decades ago but the research institute lives on (<a href="http://www.ibch.ru/en/about" target="_blank">here</a>). The difficult of biology forever endures.

[Next lesson](ab_initio){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Citations

[^1]: Wade W. 2002. Unculturable bacteria--the uncharacterized organisms that cause oral infections. Journal of the Royal Society of Medicine, 95(2), 81–83. https://doi.org/10.1258/jrsm.95.2.81

[^2]: Severe acute respiratory syndrome coronavirus 2 isolate Wuhan-Hu-1, complete genome. https://www.ncbi.nlm.nih.gov/nuccore/MN908947

[^3]: Annotated Severe acute respiratory syndrome coronavirus 2 isolate Wuhan-Hu-1, complete genome. https://go.usa.gov/xfzMM

