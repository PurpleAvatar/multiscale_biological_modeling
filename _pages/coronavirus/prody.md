---
permalink: /coronavirus/prody
title: "ProDy Tutorial"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

This is a short tutorial on how to use ProDy to calculate RMSD between two structures and perform GNM calculations. Please be sure to have the following installed:

<a href="https://www.python.org/downloads/" target="_blank">Python</a> (2.7, 3.5, or later)

<a href="http://prody.csb.pitt.edu/downloads/" target="_blank">ProDy</a>

<a href="https://numpy.org/install/" target="_blank">NumPy</a>

<a href="https://biopython.org/" target="_blank">Biopython</a>

<a href="https://ipython.org/" target="_blank">IPython</a>

<a href="https://matplotlib.org/" target="_blank">Matplotlib</a>

### Getting Started
It is recommended that you create a workspace for storing created files when using ProDy. Make sure you are in your worspace before starting up IPython.
~~~ python
ipython --pylab
~~~~~

Import functions and turn interactive mode on (only need to do this once per session).
~~~ python
In[#]: from pylab import *
In[#]: from prody import *
In[#]: ion()
~~~~~

<hr>

### RMSD Calculations

This section will be on getting RMSD values for structure comparisons. We will be matching chains between the two structures based on sequence identity and sequence overlap. The goal is to calculate the Root Mean Square Deviation scores between the alpha-Carbons of the matched chains. This will give us a basic quantitative measure of the structural differences between the two proteins. First, we will define a function that will list out matched chains for later use.
~~~ python
 In[#]: def printMatch(match):
...: print('Chain 1 : {}'.format(match[0]))
...: print('Chain 2 : {}'.format(match[1]))
...: print('Length : {}'.format(len(match[0])))
...: print('Seq identity: {}'.format(match[2]))
...: print('Seq overlap : {}'.format(match[3]))
...: print('RMSD : {}\n'.format(calcRMSD(match[0], match[1])))
...:
~~~~~

#### Parsing Protein Structures
{: .no_toc}

Next, we will parse the protein structures from PDB or from the current directory. *Note:* The protein structures need to be in *.pdb* format.
~~~ python
In[#]: struct1 = parsePDB(‘6crx’)
~~~~~~~
This will prompt the console to search for `6crx`, SARS Spike protein, from the Protein Data Bank, download the .pdb file into the current directory, and save it to the variable `struct1`.

~~~ python
In[#]: struct2 = parsePDB(‘6vxx.pdb’)
~~~~~
Including the .pdb tag will prompt the console to search for the file '6vxx.pdb' in the current directory and parse it. You can download .pdb files directly from PDB. If you do not have 6vxx.pdb, follow the format of the previous command.

#### Matching Chains
{: .no_toc}

With the protein structures parsed, we can now match chains. The default threshold for sequence identity and sequence overlap are 90%. This can be changed by specifying the desired thresholds. Here, a sequence identity threshold of 75% and an overlap threshold of 80% is specified.
~~~ python
In[#]: matches = matchChains(struct1, struct2, seqid = 75, overlap = 80)
~~~~~
Now, we will use our previously defined function to list out matched chains.
~~~ python
In[#]: for match in matches:
…: printMatch(match)
…:
~~~~~~
You should see the results listed like this:
![image-center](../assets/images/chris_RMSDResult1.png){: .align-center}

![image-center](../assets/images/chris_RMSDResult2.png){: .align-center}

The results are stored as a 2D array called `matches`, where `matches[i][j]` represents the *i*th match and *j*th chain (zero-based). Given the previous example, `matches[0][0]` corresponds to `Chain 1 : AtomMap Chain A from 6crx -> Chain A from 6vxx` and `matches[5][1]` corresponds to `Chain 2: AtomMap Chain C from 6vxx -> Chain B from 6crx`.

Let us say we want to calculate the RMSD score between the matched `Chain C` from `6crx` and `Chain A` from `6vxx`. We need to first transform and align the chains such that it minimizes the RMSD between the C⍺.
~~~ python
In[#]: first_ca = matches[6][0]
In[#]: second_ca = matches[6][1]
In[#]: calcTransformation(first_ca, second_ca).apply(first_ca);
~~~~~
Finally, we can calculate the RMSD score.
~~~ python
 In[#]: calcRMSD(first_ca, second_ca)
~~~~~~
The result should be an RMSD score of around 3.
It is also possible to merge matches to calculate the RMSD of the overall structure. In this example, both 6crx and 6vxx are each made up of three chains. Here we merge the three matches corresponding to A to A, B to B, and C to C.
~~~ python
In[#]: first_ca = matches[0][0] + matches[4][0] + matches[8][0]
In[#]: second_ca = matches [0][1] + matches[4][1] + matches[8][1]
In[#]: calcTransformation(first_ca, second_ca).apply(first_ca);
In[#]: calcRMSD(first_ca, second_ca)
~~~~~~
The result should be an RMSD score of around 11.

<hr>

<details>
 <summary>RMSD Exercise</summary>
 Try to find the RMSD score between all chain matchings in 6vxx and 6crx (i.e. A to A, A to B, A to C, B to A, etc.). Your results should look similar to this:
 
 <img src="../_pages/coronavirus/files/RMSDExercise1.png">
 
</details>

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
