---
permalink: /module_1/setup
title: "Setup"
sidebar: 
 nav: "mod1"
toc: true
toc_sticky: true
---

## Setting up Module 1

*Will be using CellBlender*

### Setting up CellBlender 
Setting up CellBlender can be done using the default tutorial with just a few changes from the original installation instructions.

Follow the instructions from the [CellBlender website](https://mcell.org/downloads/windows/install_2019_05/index.html)

**Watch out!** CellBlender is based on a legacy version of Blender. Use the following two changes to the default installation instructions. 
{: .notice--primary}

1. Instead of downloading the newest version of Blender, go to the previous versions tab...

![image-center](../assets/images/m1_image13.png){: .align-center}

...and download Blender 2.79b

2. Once Blender is downloaded,  the file path may be different from what is shown in the CellBlender tutorial- instead of *Blender/2.79/python/bin*, the pathway may be something like: *blender-2.79/2.79/python/bin*. Changing the name of the downloaded Blender folder to match the path in the tutorial may help reduce confusion. 

### Setting-up Simulations

See [CellBlender Layout](https://purpleavatar.github.io/multiscale_biological_modeling/module_1/navigation) for instructions on any underlined items. 

Step 0: 
From a new Blender file, initialize CellBlender
Delete the existing default cube by right clicking on the cube to select the cube (an orange outline should be around the cube when it is selected) and pressing the “x” key to delete
From the tab CellBlender > Model Objects, insert a new plane (follow figure S.1) 

Figure S.1 - From CellBlender > Model Objects, click on the “(+)” symbol to center the cursor. Next press the square “plane” button to create the object. To have CellBlender recognize this object as a model object, press the “+” button. The name of this object is “Plane” by default, though you can change this and edit the color by selecting the color wheel. A slightly transparent coloring will help with visibility, but is not necessary. 


Figure S.2 - Resizing the render preview window (where the objects are visible in the center of the screen) is recommended. From the View menu, select “Top” to align the view directly overhead. With the plane object selected, follow the arrow over to the object parameters menu (the orange cube) and scale the plane by setting the first two values to “1.5”. Then, hover the mouse over the object and either use the ctrl + “+” 6 times or the scroll wheel on the mouse to zoom in. 

