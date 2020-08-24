---
permalink: /coronavirus/prody
title: "ProDy"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

*Work in progress. Moving things to its own separate sections

<a href="http://prody.csb.pitt.edu/" target="_blank">ProDy</a> is an open-source Python package that allows users to perform protein structural dynamics analysis. Its flexibility allows users to select specific parts or atoms of the structure for conducting normal mode analysis and structure comparison. Please be sure to have the following installed:

<a href="https://www.python.org/downloads/" target="_blank">Python</a> (2.7, 3.5, or later)

<a href="http://prody.csb.pitt.edu/downloads/" target="_blank">ProDy</a>

<a href="https://numpy.org/install/" target="_blank">NumPy</a>

<a href="https://biopython.org/" target="_blank">Biopython</a>

<a href="https://ipython.org/" target="_blank">IPython</a>

<a href="https://matplotlib.org/" target="_blank">Matplotlib</a>

### Getting Started
It is recommended that you create a workspace for storing created files when using ProDy or storing protein .pdb files. Make sure you are in your workspace before starting up IPython.
~~~ python
ipython --pylab
~~~~~

Import functions and turn interactive mode on (only need to do this once per session).
~~~ python
In[#]: from pylab import *
In[#]: from prody import *
In[#]: ion()
~~~~~

*Will move everything under this point.

<hr>

### GNM Calculations

This section will be on performing GNM calculations and creating contact map, cross-correlation, slow mode shape, and square fluctuation plots. As the example, we will be replicating the "SARS-CoV-2 Spike Chain A" GNM results from the *Normal Mode Analysis* page of the module. Please be sure to have <a href="http://www.rcsb.org/structure/6VXX" target="_blank">6vxx.pdb</a> downloaded in the current working directory. (You can also download it directly while parsing as explained in the previous section).

First, follow the steps in the *Getting Started* section to start up IPython and import the neccessary functions.

Next, we will parse in *6vxx* and set it as the variable *spike*.
~~~ python
In[#]: spike = parsePDB('6vxx.pdb')
~~~~~

For this GNM calculation, we will focus only on the alpha-carbons of Chain A. We will create variable *calphas* with the selection.
~~~ python
In[#]: calphas = spike.select('calpha and chain A')
~~~~~

Now, we will instantiate a GNM instance and build the corresponding Kirchhoff matrix. You can pass parameters for the cutoff (threshold distance between atoms) and gamma (spring constant). The defaults are 10.0 Å and 1.0, respectively. Here, we will set the cutoff to be 20.0 Å.
~~~ python
In[#]: gnm = GNM('SARS-CoV-2 Spike (6vxx) Cutoff = 20.0 A')                 #This is the title that will appear on top of the plots
In[#]: gnm.buildKirchhoff(calphas, cutoff=20.0)
~~~~

For the creation of normal modes, the default is 20 non-zero modes. This value can be changed and zero modes can be kept if desired. e.g. *gnm.calcModes(50, zeros=True)*. We will use the default. In addition, we will create hinge sites for laster use in the slow mode shape plot.
~~~ python
In[#]: gnm.calcModes()
In[#]: hinges = gnm.getHinges()
~~~~

(Optional) Information of the GNM and Kirchhoff matrix can be pulled with the following commands.
~~~ python
In[#]: gnm.getEigvals()
In[#]: gnm.getEigvecs()
In[#]: gnm.getCovariance()

#To get information specifically on the slowest mode (which is always indexed at 0):
In[#]: slowMode = gnm[0]
In[#]: slowMode.getEigval()
In[#]: slowMode.getEigvec()
~~~~

We have now successfully created the GNM calculations and can generate the plots. Make sure to close the plot before creating another.
Contact Map:
~~~ python
In[#]: showContactMap(gnm);
~~~~
<img src="../_pages/coronavirus/files/GNMTutorial/SARS-CoV-2_ChainA_Contact_20A.png">

Cross-correlations:
~~~ python
In[#]: showCrossCorr(gnm);
~~~~
<img src="../_pages/coronavirus/files/GNMTutorial/SARS-CoV-2_ChainA_CrossCorr_20A.png">

Slow Mode Shape:
~~~ python
In[#]: showMode(gnm[0], hinges=True)
In[#]: grid();
~~~~~
<img src="../_pages/coronavirus/files/GNMTutorial/SARS-CoV-2_ChainA_SlowMode_20A.png">

Square Fluctuations
~~~ python
In[#]: showSqFlucts(gnm[0], hinges=True);
~~~~
<img src="../_pages/coronavirus/files/GNMTutorial/SARS-CoV-2_ChainA_SqFlucts_20A.png">

<hr>

<details>
 <summary>GNM Exercise</summary>
 Try to produce the GNM plots of SARS Spike Chain A. Use the pdb file <a href="https://www.rcsb.org/structure/5XLR" target="_blank">5xlr</a> and 20 Å cutoff. Your results should look similar to this:
 
 <img src="../_pages/coronavirus/files/GNMTutorial/GNMExercise1.png">
 
</details>


[Conclusion](conclusion){: .btn .btn--primary .btn--x-large} [VMD Tutorial](VMDTutorial){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}
