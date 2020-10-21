---
permalink: /prologue/tutorial-diffusion
title: "Software Tutorial: Building a Diffusion Cellular Automaton with Jupyter Notebook"
sidebar:
 nav: "prologue"
 nav: "prologue"
toc: true
toc_sticky: true
---

**NOTE**: You will need to place this file on the same level as another folder named "*/dif_images*". ImageIO will not always create this folder automatically, so it may need to be created manually.

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


## Diffusion Jupyter Notebook Tutorial

In this Jupyter notebook, we will be simulating diffusion with two particle species. We will be using the Gray-Scott model which has only two variables: a prey and a predator. Predator eats the prey to multiply and prey is present in the environment constantly. However,  we will omit the interactions between these two molecules for now and only show the diffusion.

~~~ python
import matplotlib.pyplot as plt
import numpy as np
import time
from scipy import signal
import imageio

%matplotlib inline

images = []
~~~

Here we introduce a **convolution function** which uses a **laplacian**. The convolve function will use our specified laplacian matrix to simulate diffusion. The laplacian describes the change in our matrix as we saw in the Gray-Scott Model page. See the [Gray-Scott Jupyter Notebook](https://purpleavatar.github.io/multiscale_biological_modeling/prologue/gs-jupyter) for a more detailed explanation.

~~~ python
def simulate(numIter, A, B, f, k, dt, dA, dB, lapl, plot_iter):
    print("Running Simulation")
    start = time.time()

    # Run the simulation
    for iter in range(numIter):
        A_new = A + (dA * signal.convolve2d(A, lapl, mode='same', boundary='fill', fillvalue=0)) * dt
        B_new = B + (dB * signal.convolve2d(B, lapl, mode='same', boundary='fill', fillvalue=0)) * dt
        A = np.copy(A_new)
        B = np.copy(B_new)
        if (iter % plot_iter is 0):
            plt.clf()
            plt.imshow((B / (A+B)),cmap='Spectral')
            plt.axis('off')
            now = time.time()
            # print("Seconds since epoch =", now-start)
            # plt.show()
            filename = 'dif_images/diffusion_'+str(iter)+'.png'
            plt.savefig(filename)
            images.append(imageio.imread(filename))

    return A, B
~~~

The following parameters will set up our problem space by defining the grid size, the number of iterations we will range through , and where the predators and prey will start.

~~~ python
# _*_*_*_*_*_*_*_*_* GRID PROPERTIES *_*_*_*_*_*_*_*_*_*
grid_size = 101 # Needs to be odd
numIter = 10000;
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
dA = 0.5
dB = 0.25
lapl = np.array([[0.05, 0.2, 0.05],[0.2, -1.0, 0.2],[0.05, 0.2, 0.05]])
plot_iter = 50

simulate(numIter, A, B, f, k, dt, dA, dB, lapl, plot_iter)
imageio.mimsave('dif_images/0diffusion_movie.gif', images)
~~~

You should get images similar to the ones below. If you would like to see more images, you can adjust the *plot_iter* variable or *numIter* variable which controls how often the graph is plotted and how many iterations are in the simulation.

<iframe width="640" height="360" src="../assets/0diffusion_movie.gif" frameborder="0" allowfullscreen></iframe>

[Return to main text](animals##Changing-parameters-influence-the-macro-behavior-of-the-reaction-diffusion-system){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
