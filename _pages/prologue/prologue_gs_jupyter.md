---
permalink: /prologue/gs-jupyter
title: "Software Tutorial: Implementing the Gray-Scott Model for Coarse-Grained Reaction-Diffusion with Jupyter Notebook"
sidebar:
 nav: "prologue"
 nav: "prologue"
---

The following tutorial will use a Jupyter Notebook to implement the Gray-Scott model. It requires a familiarity with Python, and installation instructions can be found in our coarse-grained [diffusion tutorial](tutorial-diffusion). If you are interested in downloading the completed notebook, please click <a href="../downloads/Gray-Scott_Reaction_Diffusion_Model.ipynb" download="Gray-Scott_Reaction_Diffusion_Model.ipynb">here</a>.

Assuming you have Jupyter notebook, create a new file called `gray-scott.ipynb` (you may instead want to duplicate and modify your `diffusion_automaton.ipynb` file from the diffusion tutorial). **Note**: You should make sure to save this notebook on the same level as another folder named `/dif_images`. ImageIO will not always create this folder automatically, so you may need to create it manually.

At the top of the notebook, we need the following imports and declarations.

~~~ python
import matplotlib.pyplot as plt
import numpy as np
import time
from scipy import signal
import imageio

%matplotlib inline

'''
simulate function
Description: Simulate the Gray-Scott model for numIter iterations.
Inputs:
    - numIter:  number of iterations
    - A:        prey matrix
    - B:        predator matrix
    - f:        feed rate
    - k:        kill rate
    - dt:       time constant
    - dA:       prey diffusion constant
    - dB:       predator diffusion constant
    - Lapl:     Laplacian matrix to calculate diffusion

Outputs:
    - A_matrices:   Prey matrices over the course of the simulation
    - B_matrices:   Predator matrices over the course of the simulation
'''
~~~

The next step takes in the parameters for the simulation in order to iterate through each grid which will be printed down below.

POINT BACK TO DIFFUSION TUTORIAL

~~~ python
images = []

def simulate(numIter, A, B, f, k, dt, dA, dB, lapl, plot_iter):
    print("Running Simulation")
    start = time.time()

    # Run the simulation
    for iter in range(numIter):
        A_new = A + (dA * signal.convolve2d(A, lapl, mode='same', boundary='fill', fillvalue=0) - (A * B * B) + (f * (1-A))) * dt
        B_new = B + (dB * signal.convolve2d(B, lapl, mode='same', boundary='fill', fillvalue=0) + (A * B * B) - ((k + f) * B)) * dt
        A = np.copy(A_new)
        B = np.copy(B_new)
        if (iter % plot_iter is 0):
            plt.clf()
            plt.imshow((B / (A+B)),cmap='Spectral')
            plt.axis('off')
            now = time.time()
            # print("Seconds since epoch =", now-start)
            # plt.show()
            filename = 'gs_images/gs_'+str(iter)+'.png'
            plt.savefig(filename)
            images.append(imageio.imread(filename))

    return A, B
~~~

The following parameters will set up our problem space by defining the grid size, the number of iterations we will range through , and where the predators and prey will start.

~~~ python
# _*_*_*_*_*_*_*_*_* GRID PROPERTIES *_*_*_*_*_*_*_*_*_*
grid_size = 101 # Needs to be odd
numIter = 5000;
seed_size = 11 # Needs to be an odd number
A = np.ones((grid_size,grid_size))
B = np.zeros((grid_size,grid_size))

# Seed the predators
B[int(grid_size/2)-int(seed_size/2):int(grid_size/2)+int(seed_size/2)+1, \
int(grid_size/2)-int(seed_size/2):int(grid_size/2)+int(seed_size/2)+1] = \
np.ones((seed_size,seed_size))
~~~

The following parameters will control how the predator and prey interact with each other.

~~~ python
# _*_*_*_*_*_*_*_*_* SIMULATION VARIABLES *_*_*_*_*_*_*_*_*_*
f = 0.055
k = 0.062
dt = 1.0
dA = 1.0
dB = 0.5
lapl = np.array([[0.05, 0.2, 0.05],[0.2, -1.0, 0.2],[0.05, 0.2, 0.05]])
plot_iter = 50
~~~

Now we can run the program and view the simulations.

~~~ python
simulate(numIter, A, B, f, k, dt, dA, dB, lapl, plot_iter)
imageio.mimsave('gs_images/gs_movie.gif', images)
~~~

You should get images similar to the ones below. If you would like to see more images, you can adjust the *plot_iter* variable or *numIter* variable which controls how often the graph is plotted and how many iterations are in the simulation.

![image-center](../assets/images/gray_scott_jupyter_1.png)
![image-center](../assets/images/gray_scott_jupyter_2.png)
![image-center](../assets/images/gray_scott_jupyter_3.png){: .align-center}

A great follow up would be to use a gif library package for python, such as Pillow or ImageIO. https://stackoverflow.com/questions/753190/programmatically-generate-video-or-animated-gif-in-python

<iframe width="640" height="360" src="../assets/gs_movie.gif" frameborder="0" allowfullscreen></iframe>
