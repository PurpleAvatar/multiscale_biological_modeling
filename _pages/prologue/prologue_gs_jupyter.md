---
permalink: /prologue/gs-jupyter
title: "Gray Scott Jupyter Notebook"
sidebar:
 nav: "prologue"
 nav: "prologue"
toc: true
toc_sticky: true
---

## Setting Up

The following tutorial will walk through a Jupyter Notebook, which can be downloaded <a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/Gray-Scott_Reaction_Diffusion_Model.ipynb" download="Gray-Scott_Reaction_Diffusion_Model.ipynb">here</a>.

**NOTE**: You will need to place this file on the same level as another folder named "/gs_images". ImageIO will not always create this folder automatically, so it may need to be created manually.
{: .notice--primary}

The following software and packages will need to be installed:

| Installation Link | Version[^version] | Check Install | 
|:------|:-----:|------:|
| [Python3](https://www.python.org/downloads/)  |3.7 |*python --version* | 
| [Jupyter Notebook](https://jupyter.org/index.html) | 4.4.0 | *jupyter --version* |
| [matplotlib](https://matplotlib.org/users/installing.html) | 2.2.3 | *conda list* or *pip list* |
| [numpy](https://numpy.org/install/) | 1.15.1 | *conda list* or *pip list* |
| [scipy](https://www.scipy.org/install.html) |  1.1.0 | *conda list* or *pip list* |
| [imageio](https://imageio.readthedocs.io/en/stable/installation.html) | 2.4.1 | *conda list* or *pip list* |

[^version]: Other versions may be compatible with this code, but those listed are known to work for this tutorial

You can read more about various installation options [here](https://realpython.com/installing-python/) or [here](https://docs.conda.io/en/latest/). 

## Gray-Scott Jupyter Notebook Tutorial

In this Jupyter notebook, we will be simulating a Turing pattern generator, called the Gray-Scott Reaction-Diffusion model. Gray-Scott model is a model that has only two variables: a prey and a predator. Predator eats the prey to multiply and prey is present in the environment constantly.

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

To calculate these changes, we use a **convolve** function and a **laplacian**. The convolve function in this case takes two matrices, *A* and *lapl*, and uses *lapl* as a set of multipliers for each square in the matrix. We can see this operation in action in the image below. 

![image-center](../assets/images/convolution.PNG){: .align-center}
A single step in the convolution function which takes the first matrix and adds up each cell multiplied by the number in the second matrix. Here we see (0 * 0) + (2 * ¼) + (0 * 0) + (3 * ¼) + (1 * -1) + (2 * ¼) + (1 * 0) + (1 * ¼) +(1 * 0) = 1
{: .text-center}

Our matrix *lap1* is a laplacian because it describes the gradient, or change over time, for each point in the matrix (not to be confused with a “graph Laplacian”). Because we’re trying to describe the rate of diffusion over this system, the values in the laplacian excluding the center sum to 1. In our code, the value in the center is -1 because we’ve specified the *change* in the system with the convolution function i.e. the matrix *dA*, which we then add to the original matrix *A*. Thus the total sum of the laplacian is 0 which means the total change in number of molecules due to diffusion is 0, even if the molecules are moving to new locations. We don’t want any new molecules created due to just diffusion! 

As an additional note, why not just have the center of the laplacian stay 0 and not use dA? While using dA, we can easily specify a time step *dt* < 1  which allows us to take smaller steps in the diffusion reaction for a more accurate simulation. Remember that the larger our approximation for each time step, the more information we might be losing in our model. This is part of the accuracy vs. efficiency tradeoff in modeling! 

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