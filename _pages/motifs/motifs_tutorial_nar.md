---
permalink: /motifs/tutorial_nar
title: "NAR"
sidebar: 
 nav: "motifs"
toc: true
toc_sticky: true
---

*Once CellBlender is installed and set-up, we can take a look at how ...something about NAR, motivations for NAR.*

### A Cell's Response

*Some motivation about how a cell needs to produce something, perhaps as a signal response. What are requirements for production? Fast production.*

### Non-NAR (Non-Negative Auto-Regulation)

Go to CellBlender > Molecules and create the following molecules:

![image-center](../assets/images/motifs_norm1.png){: .align-center}

Select CellBlender > Molecules
Create a molecule by clicking the “+” button
Optional: change the color
Rename the molecule “Y” 
Change molecule type to “Surface Molecule” 
Change the diffusion constant to “1e-6”
Change the scale factor to “5.0” 

![image-center](../assets/images/motifs_norm2.png){: .align-center}

Create another  molecule named “Hidden”
Set the molecule type to “Surface Molecule”  and the diffusion constant to “1e-6”

Go to CellBlender > Molecule Placement to set the following options; 

![image-center](../assets/images/motifs_norm3.png){: .align-center}

Select CellBlender > Molecule Placement
Add a new release site by pressing the “+” button 
Select the Molecule “Hidden” 
Type in the name of the Model Object “Plane” (or custom name set in fig. S.1
Set the Quantity to Release to 300 

Go to CellBlender > Reactions to create the following reactions:

![image-center](../assets/images/motifs_norm4.png){: .align-center}

Select CellBlender > Reactions
Add a new reaction by pressing the “+” button 
Under Reactants, type “ Hidden’ “. Note: the apostrophe is required to indicate the directionality of a surface molecule.  
Under Products, type “ Hidden’ + Y’ “. 
Set the Forward Rate to “2e2”

![image-center](../assets/images/motifs_norm5.png){: .align-center}

Add a new reaction by pressing the “+” button 
Under Reactants, type “ Y’ “. 
Under Products, type “ NULL“. 
Set the Forward Rate to “3e2”

Go to CellBlender > Plot Output Settings to set up a plot as follows: 

![image-center](../assets/images/motifs_norm6.png){: .align-center}

Select CellBlender > Plot Output Settings
Add a new plot by pressing the “+” button 
Under molecule, select  “Y”
If not already selected, choose “Java Plotter” for the plot method.
Optional: select “Molecule Colors” to match the same colors in the plot as the molecules in the animation

Go to CellBlender > Run Simulation and select the following options: un Simulation using 12000 frames, which should take less than 5 seconds to finish

![image-center](../assets/images/motifs_norm6.png){: .align-center}

Select CellBlender > Run Simulation
Change the number of iterations to “12,000”
Click “Export & Run”

Press the CellBlender > Reload Visualization Data button 

![image-center](../assets/images/motifs_norm6.png){: .align-center}

Fig. NN.1 - After pressing the Reload Visualization Data button, the animated simulation can be played using the buttons at the bottom of the screen. The timeline represents each frame of animation, which should now show 12,000 frames.

Go back to CellBlender > Plot Output Settings and click the plot button. NOTE: if no plot displays, see [additional instructions on trying other plotters or the jupyter notebook]

![image-center](../assets/images/motifs_norm9.png){: .align-center}

![image-center](../assets/images/motifs_norm_graph.png){: .align-center}

Fig. NN.2 - The plot above should be displayed when completing the No-NAR tutorial

Save your file as “CellBlender_Non_NAR_test.blend” 

### NAR (Negative Auto-Regulation)

*What if a cell needs a faster response? Could just increase the rate of production, but that would lead to higher steady state (can test on own). Simplest way? Common mechanism- NAR*

See “Setting-up Simulations” before starting these steps

Quick Tutorial: 
Load the file from Non-NAR tutorial
Add the following reactions
Change Hidden’ -> Hidden’ + Y’ to a forward rate of 1e3
Y’ + Y’ →  Y’   with a forward rate of 1e2

![image-center](../assets/images/motifs_nar_graph.png){: .align-center}

*Now we can compare visuals on the graphs and see how much faster for the same steady state*

[Previous](navigation){: .btn .btn--primary .btn--x-large} [Next Page](tutorial_feed){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


