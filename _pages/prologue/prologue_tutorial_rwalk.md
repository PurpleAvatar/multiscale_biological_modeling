---
permalink: /prologue/tutorial-random-walk
title: "Simulating particle diffusion with CellBlender"
sidebar:
 nav: "prologue"
 nav: "prologue"
toc: true
toc_sticky: true
---

## Setting up CellBlender
Setting up CellBlender can be done using the default tutorial with just a few changes from the original installation instructions.

First, follow the instructions from the [CellBlender website](https://mcell.org/downloads/windows/install_2019_05/index.html), with the following disclaimer.

**Important:** CellBlender requires a previous version of Blender. Use the following two changes to the default installation instructions.
{: .notice--primary}

First, instead of downloading the newest version of Blender, go to the previous versions tab...

![image-center](../assets/images/motifs_website.png){: .align-center}

...and download Blender 2.79b.

Second, once Blender is downloaded,  the file path may be different from what is shown in the CellBlender tutorial- instead of *Blender/2.79/python/bin*, the pathway may be something like: *blender-2.79/2.79/python/bin*. Changing the name of the downloaded Blender folder to match the path in the tutorial may help reduce confusion.

## Setting-up CellBlender simulations

From a new Blender file, initialize CellBlender. Delete the existing default cube by right-clicking on the cube to select the cube (an orange outline should be around the cube when it is selected) and pressing the “x” key to delete. Then, in the tab `CellBlender > Model Objects`, insert a new plane, following the figure below.

![image-center](../assets/images/motifs_setup1.png){: .align-center}
In `CellBlender > Model Objects`, click on the `+` symbol to center the cursor. Next press the square “plane” button to create the object. To have CellBlender recognize this object as a model object, press the `+` button. The name of this object is `Plane` by default, although you can change this name and edit the color by selecting the color wheel if you like. A slightly transparent coloring will help with visibility but is not necessary.
{: style="font-size: medium;"}

Resizing the render preview window so that objects are visible in the center of the screen is recommended. See the following figure for instructions. Then save your file as `CellBlender_Tutorial_Template.blend`.

![image-center](../assets/images/motifs_setup2.png){: .align-center}
From the View menu, select `Top` to align the view directly overhead. With the plane object selected, follow the arrow over to the object parameters menu (the orange cube) and scale the plane by setting the first two values to “1.5”. Then, hover the mouse over the object and either use ctrl + “+” 6 times or the scroll wheel on your mouse to zoom in.
{: style="font-size: medium;"}

## CellBlender layout

This section will provide images and descriptions for the different components of the Blender window. When a new file has been created, the following figure shows the menu options available.

![image-center](../assets/images/motifs_nav1.png){: .align-center}

**A:** This is the window for modules like CellBlender. To start CellBlender, you must click on the `CellBlender` tab and then click the `Initialize CellBlender` button as shown in the image. This will then display the image shown as “D” in the figure below.

**B:** There are many `View` tabs throughout the Blender window. Any future tutorials referring to the `View` tab are referencing this tab.

**C:** This window contains options relating to a selected object.

![image-center](../assets/images/motifs_nav2.png){: .align-center}

**D:** This is the CellBlender menu, which contains sub-menus which will be noted as follows: `CellBlender > Model Objects`. We recommend dragging the edge of the window outward to increase visibility (see box “e” on the image).

## CellBlender and the random walk

Load up the `CellBlender_Tutorial_Template.blend` file from the previous section and save your file as `random_walk.blend`.

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
