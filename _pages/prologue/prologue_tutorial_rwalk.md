---
permalink: /prologue/tutorial-random-walk
title: "Random Walk Tutorial"
sidebar:
 nav: "prologue"
 nav: "prologue"
toc: true
toc_sticky: true
---

## CellBlender and the Random Walk

Load in the CellBlender_Tutorial_Template from (Link to Setting up CellBlender). Save as *random_walk.blend*

![image-center](../assets/images/cellblender_location.png){: .align-center}

Right click on the plane object to ensure it is selected. Go to the object parameters menu (the orange cube) and move the plane by setting the third *location* value to 1.0 instead of 0.0

Go to *CellBlender > Molecules* and create the following molecules:

![image-center](../assets/images/motifs_norm1.png){: .align-center}

1. Click on the plus button
2. Select a color (such as orange)
3. Name the molecule “X” 
4. Select the molecule type as “Surface Molecule”
5. Add a diffusion constant of “1e-6”
6. Up the scale factor to 5 (click and type “5” or use the arrows)

Now go to *CellBlender > Molecule Placement* to set the following sites: 

![image-center](../assets/images/motifs_norm3.png){: .align-center}

1. Click on the plus button
2. Select or type in the molecule “X”
3. Type in the name of the Object/Region “Plane”
4. Set the Quantity to Release as “1” 

Go to *CellBlender > Run Simulation* and select the following options: 

![image-center](../assets/images/motifs_norm7.png){: .align-center}

1. Set the number of iterations to “1000”
2. Ensure the time step is set as “1e-6”
3. Click Export & Run

Click on *CellBlender > Reload Visualization Data* 

![image-center](../assets/images/motifs_norm8.png){: .align-center}

Save this file

You have the option of watching the animation within the Blender window by clicking the play button at the bottom of the screen.

You can also save and export this movie with the following steps: 

![image-center](../assets/images/cellblender_render.png){: .align-center}

Click on the movie tab
Scroll down to the file name
Select a suitable location for the file 
Select the FFmpeg_video file format or whatever type works best for you
Click on *Render > OpenGL Render Animation*

The movie will begin playing through, and when the animation is complete the movie file should be in the folder location you selected. 


[Return to main text](random-walk#Ensuring-the-same-steady-state-concentration){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
