---
permalink: /module_1/start
title: "Module 1"
sidebar: 
 nav: "mod1"
toc: true
toc_sticky: true
---

No class with TOC looks like this

Biological networks and extending our particle simulators to answer questions about "why" and "how" unintelligent systems can build nontrivial systems

**Watch out** file, but this text has something special on the next line so it looks like this
{: .notice--primary}

But, can images be used easily here? 

![gras](assets/images/bio-photo.jpg)

![image-center](../assets/images/m1_image1.png){: .align-center}



## Instructions for CellBlender Simulations 

These instructions will be placed on a website with the intention of walking students through the basics of the  CellBlender software and biochemical concepts building off of the previous module on gene regulatory networks. The descriptions of each simulation and teaching material is temporarily absent; this is just a tutorial for creating the simulations on CellBlender.

### Setting up CellBlender 
Setting up CellBlender can be done using the default tutorial with just a few changes from the original installation instructions.

Follow the instructions from the CellBlender website: https://mcell.org/downloads/windows/install_2019_05/index.html

With the following two changes: 

1. Instead of downloading the newest version of Blender, go to the previous versions tab...
![image-center](../assets/images/m1_image13.png){: .align-center}
...and download Blender 2.79b

2. Once Blender is downloaded,  the file path may be different from what is shown in the CellBlender tutorial- instead of *Blender/2.79/python/bin*, the pathway may be something like: *blender-2.79/2.79/python/bin*. Changing the name of the downloaded Blender folder to match the path in the tutorial may help reduce confusion. 

### CellBlender Layout

When a new file has been created, the following shows the menu options available: 
![image-center](../assets/images/m1_image3.png){: .align-center}
A. This is the window for modules like CellBlender. To start CellBlender, you must click on the “CellBlender” tab and then click the “Initialize CellBlender” button as shown in the image. This will then display the image shown in “D” 
B. There are many “View” tabs throughout the Blender window. When referring to the “View” tab in future tutorials,  this is the one which will be referenced. 
C. This window contains many options relating to a selected object. 

![image-center](../assets/images/m1_image12.png){: .align-center}
D. This is the CellBlender menu, which contains sub-menus which will be noted as follows: CellBlender > Model Objects. It is recommended that the edge of the window is dragged outward to increase visibility (see box “e” on the image) 

### Setting-up Simulations

See “CellBlender Layout” for instructions on any underlined items. 
Step 0: 
From a new Blender file, initialize CellBlender
Delete the existing default cube by right clicking on the cube to select the cube (an orange outline should be around the cube when it is selected) and pressing the “x” key to delete
From the tab CellBlender > Model Objects, insert a new plane (follow figure S.1) 

Figure S.1 - From CellBlender > Model Objects, click on the “(+)” symbol to center the cursor. Next press the square “plane” button to create the object. To have CellBlender recognize this object as a model object, press the “+” button. The name of this object is “Plane” by default, though you can change this and edit the color by selecting the color wheel. A slightly transparent coloring will help with visibility, but is not necessary. 


Figure S.2 - Resizing the render preview window (where the objects are visible in the center of the screen) is recommended. From the View menu, select “Top” to align the view directly overhead. With the plane object selected, follow the arrow over to the object parameters menu (the orange cube) and scale the plane by setting the first two values to “1.5”. Then, hover the mouse over the object and either use the ctrl + “+” 6 times or the scroll wheel on the mouse to zoom in. 

### Rules for Non-NAR (Non-Negative Auto-Regulation)

Go to CellBlender > Molecules and create the following molecules:


Select CellBlender > Molecules
Create a molecule by clicking the “+” button
Optional: change the color
Rename the molecule “Y” 
Change molecule type to “Surface Molecule” 
Change the diffusion constant to “1e-6”
Change the scale factor to “5.0” 



Create another  molecule named “Hidden”
Set the molecule type to “Surface Molecule”  and the diffusion constant to “1e-6”

Go to CellBlender > Molecule Placement to set the following options; 


Select CellBlender > Molecule Placement
Add a new release site by pressing the “+” button 
Select the Molecule “Hidden” 
Type in the name of the Model Object “Plane” (or custom name set in fig. S.1
Set the Quantity to Release to 300 

Go to CellBlender > Reactions to create the following reactions:


Select CellBlender > Reactions
Add a new reaction by pressing the “+” button 
Under Reactants, type “ Hidden’ “. Note: the apostrophe is required to indicate the directionality of a surface molecule.  
Under Products, type “ Hidden’ + Y’ “. 
Set the Forward Rate to “2e2”


Add a new reaction by pressing the “+” button 
Under Reactants, type “ Y’ “. 
Under Products, type “ NULL“. 
Set the Forward Rate to “3e2”

Go to CellBlender > Plot Output Settings to set up a plot as follows: 


Select CellBlender > Plot Output Settings
Add a new plot by pressing the “+” button 
Under molecule, select  “Y”
If not already selected, choose “Java Plotter” for the plot method.
Optional: select “Molecule Colors” to match the same colors in the plot as the molecules in the animation

Go to CellBlender > Run Simulation and select the following options: un Simulation using 12000 frames, which should take less than 5 seconds to finish


Select CellBlender > Run Simulation
Change the number of iterations to “12,000”
Click “Export & Run”


Press the CellBlender > Reload Visualization Data button 

Fig. NN.1 - After pressing the Reload Visualization Data button, the animated simulation can be played using the buttons at the bottom of the screen. The timeline represents each frame of animation, which should now show 12,000 frames.

Go back to CellBlender > Plot Output Settings and click the plot button. NOTE: if no plot displays, see [additional instructions on trying other plotters or the jupyter notebook]
 


Fig. NN.2 - The plot above should be displayed when completing the No-NAR tutorial

Save your file as “CellBlender_Non_NAR_test.blend” 

### Rules for NAR (Negative Auto-Regulation)

See “Setting-up Simulations” before starting these steps

Quick Tutorial: 
Load the file from Non-NAR tutorial
Add the following reactions
Change Hidden’ -> Hidden’ + Y’ to a forward rate of 1e3
Y’ + Y’ →  Y’   with a forward rate of 1e2


### Rules for Feedforward Loop

See “Setting-up Simulations” before starting these steps

Quick Tutorial: 
Load the file from Non-NAR tutorial
Change the Y molecule to have a diffusion constant of 2e-6
Add the following molecules
Change Y to a diffusion constant of 2e-6
X, diffusion constant of 2e-6
Z, diffusion constant of 2e-6
Add the following reactions
Hidden' -> Hidden' + X', rate: 4e2
X' -> X' + Y', rate: 5e2
X' -> X' + Z', rate: 1e3
Y' + Z' -> Y', rate: 3e4
X' -> NULL, rate: 1e3
Y' -> NULL, rate: 3e2
Z' -> NULL, rate: 5e2
Hidden’ -> NULL, 3e3


### Rules for Dampened Oscillations 

See “Setting-up Simulations” before starting these steps

Quick Tutorial: 
Load the file from Non-NAR tutorial
Change the Y molecule to have a diffusion constant of 2e-6
Add the following molecules
X, diffusion constant of 2e-6
Add the following reactions
Hidden' > Hidden' + X', rate: 4e2
X' > X' + Y' , rate: 5e2
Y' + X' > Y' , rate: 2e2
X' > NULL, rate: 1e3
Y' > NULL, rate: 3e2



