---
permalink: /prologue/turing-cellblender
title: "Turing Patterns CellBlender"
sidebar:
 nav: "prologue"
 nav: "prologue"
toc: true
toc_sticky: true
---

Load in the CellBlender_Tutorial_Template from the [Random Walk Tutorial](https://purpleavatar.github.io/multiscale_biological_modeling/prologue/tutorial-random-walk). Save as *det_gray_scott.blend*

Go to *CellBlender > Molecules* and create the following molecules:

![image-center](../assets/images/motifs_norm1.png){: .align-center}

1. Click on the plus button
2. Select a color (such as red)
3. Name the molecule “predator” 
4. Under “molecule type”, select “surface molecule” 
5. Add a diffusion constant of “3e-6”
6. Up the scale factor to 2 (click and type “5” or use the arrows)

Repeat the above steps to make sure the follow molecules are entered: 

| Molecule Name | Molecule Type | Color | Diffusion Constant| Scale Factor|
|:--------|:-------:|--------:|--------:|--------:|
| predator  | Surface | Red | 1e-6  | 3|
| prey  | Surface  | Green | 1e-6  | 3 |
| A  | Surface  | Blue | 1e-6  | 0 |


Now go to *CellBlender > Molecule Placement* to set the following sites: 

![image-center](../assets/images/motifs_norm3.png){: .align-center}

1. Click on the plus button
2. Select or type in the molecule “A”
3. Type in the name of the Object/Region “Plane”
4. Set the Quantity to Release as “1000” 

Repeat the above steps to make sure the following molecules are entered

| Molecule Name | Object/Region|Quantity to Release|
|:--------|:-------:|--------:|
| A  | Plane | 1000 |
| prey | Plane | 6000 |

Placement site of the predators should be very specific, and cannot be set using the Molecule Placement tab. Hence, it is necessary to write a script for their placement. In order to do so, we will need the following Python script:

~~~ python
   import cellblender as cb
   dm = cb.get_data_model()
   mcell = dm['mcell']
   rels = mcell['release_sites']
   rlist = rels['release_site_list']
   point_list = []
   for x in range(10):
     for y in range(10):
         point_list.append([x/100,y/100,0.0])
   for x in range(10):
     for y in range(10):
         point_list.append([x/100 - 0.5,y/100 - 0.5,0.0])
   for x in range(10):
     for y in range(10):
         point_list.append([x/100 - 0.8,y/100,0.0])
   for x in range(10):
     for y in range(10):
         point_list.append([x/100 + 0.8,y/100 - 0.8,0.0])
   new_rel = {
     'data_model_version' : "DM_2015_11_11_1717",
     'location_x' : "0",
     'location_y' : "0",
     'location_z' : "0",
     'molecule' : "predator",
     'name' : "pred_rel",
     'object_expr' : "arena",
     'orient' : "'",
     'pattern' : "",
     'points_list' : point_list,
     'quantity' : "400",
     'quantity_type' : "NUMBER_TO_RELEASE",
     'release_probability' : "1",
     'shape' : "LIST",
     'site_diameter' : "0.01",
     'stddev' : "0"
   }
   rlist.append ( new_rel )
   cb.replace_data_model ( dm )
~~~ 

Locate the Outliner pane on the top-right of the Blender screen. On the left of the view button in the Outliner pane, there is a code tree icon. 

Click on this icon and choose *Text Editor*. In order to create a new file for our code, click the plus button. Copy and paste the code into the text editor and save it with the name pred-center.py. 

Next go to *CellBlender > Scripting > Data-Model Scripting > Run Script*

![image-center](../assets/images/outliner_script.PNG){: .align-center}

Select “Internal” from the Data-Model Scripting menu and click the refresh button
Click on the filename entry area next to “File” and enter *pred_center.py*. 
Click on “Run Script”

You should now have another placement iste called “pred_rel” in the *Molecule Placement Tab*

Next go to *CellBlender > Reactions* to create the following reactions: 

![image-center](../assets/images/motifs_norm4.png){: .align-center}

1. Click on the plus button
2. Under reactants, type “A;” (NOTE the semi-colon)
3. Under products, type “A; + prey;” 
4. Set the forward rate as “1e5”

Repeat the above steps for the following reactions

| Reactants |Products|Forward Rate|
|:--------|:-------:|--------:|
| A;  | A; + prey; | 1e5 |
| predator;  | NULL | 1e5 |
| predator; + predator; + prey;  | predator; + predator; + predator; | 1e1 |


Go to *CellBlender > Run Simulation* and select the following options: 

![image-center](../assets/images/motifs_norm7.png){: .align-center}

1. Set the number of iterations to “200”
2. Ensure the time step is set as “1e-6”
3. Click Export & Run

Click on *CellBlender > Reload Visualization Data* 

![image-center](../assets/images/motifs_norm8.png){: .align-center}

Save this file

You have the option of watching the animation within the Blender window by clicking the play button at the bottom of the screen.

You can also save and export this movie with the following steps: 

![image-center](../assets/images/cellblender_render.png){: .align-center}

1. Click on the movie tab
2. Scroll down to the file name
3. Select a suitable location for the file 
4. Select the FFmpeg_video file format or whatever type works best for you
5. Click on *Render > OpenGL Render Animation*

The movie will begin playing through, and when the animation is complete the movie file should be in the folder location you selected. 

[Return to main text](blocks##Reflection-on-the-Gray-Scott-model){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
