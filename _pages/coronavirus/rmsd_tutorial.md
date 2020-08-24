---
permalink: /coronavirus/rmsd2
title: "Calculating RMSD"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---
## How to Calculate RMSD

Make sure to have installed ProDy and other necessary packages. If you have not, please follow the instructions in the <a href="prody">ProDy Tutorial</a>.

In your terminal, go to your desired workspace directory and input the following command to start up IPython.
~~~ python
ipython --pylab
~~~~~

Import functions and turn interactive mode on (only need to do this once per session).
~~~ python
In[#]: from pylab import *
In[#]: from prody import *
In[#]: ion()
~~~~~

We will be matching chains between the two structures based on sequence identity and sequence overlap. The goal is to calculate the Root Mean Square Deviation scores between the alpha-Carbons of the matched chains. This will give us a basic quantitative measure of the structural differences between the two proteins. First, we will define a function that will list out matched chains for later use.
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

Next, we will parse the protein structures from PDB or from the current directory. *Note:* The protein structures need to be in *.pdb* format.
~~~ python
In[#]: struct1 = parsePDB(‘6crx’)
~~~~~~~
This will prompt the console to search for `6crx`, SARS Spike protein, from the Protein Data Bank, download the .pdb file into the current directory, and save it to the variable `struct1`.

~~~ python
In[#]: struct2 = parsePDB(‘6vxx.pdb’)
~~~~~
Including the .pdb tag will prompt the console to search for the file '6vxx.pdb' in the current directory and parse it. You can download .pdb files directly from PDB. If you do not have 6vxx.pdb, follow the format of the previous command.

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

## Assessing Our SARS-CoV-2 Models

In the <a href="modeling_tutorial">modeling tutorial</a>, we used three protein structure prediction software to create models of the S protein. For each of the three types of predicted models, the RMSD between each other, SARS-CoV-2 structures from PDB, and SARS structures from PDB were calculated using ProDy. Along with the SWISS models, five predicted models of the entire Spike protein that were released by <a href="https://boinc.bakerlab.org/" target="_blank">Rosetta@Home</a> to the *Seattle Structural Genomics Center for Infectious Disease* (SSGCID) were also assessed. Because these SSGCID models were produced using greater computational power than SWISS, comparing the RMSD of the two sets of models will provide more insight on the effect of computational power on accuracy. The SSGCID models can be found <a href="https://www.ssgcid.org/cttdb/molecularmodel_list/?target__icontains=BewuA" target="_blank">here</a>. The published PDB models are as follows: <a href="https://www.rcsb.org/structure/6vxx" target="_blank">6vxx</a> (for SARS-CoV-2 whole Spike and single chain), <a href="https://www.rcsb.org/structure/6CRX" target="_blank">6crx</a> (for SARS whole Spike and single chain), <a href="https://www.rcsb.org/structure/6lzg" target="_blank">6lzg</a> (for SARS-CoV-2 RBD), and <a href="https://www.rcsb.org/structure/6waq" target="_blank">6waq</a> (for SARS RBD).

For whole Spike modeling, the RMSD between SARS-CoV-2 and SARS is 11.368. Looking at the SWISS models, the best performing model with SARS-CoV-2 is 5.8518, while the worst is 11.3432. In comparison, the best performing SSGCID model to 6vxx is 2.08537 and the worst being 4.9636.

<img src="../_pages/coronavirus/files/RMSD_result/Swiss.png">

<hr>

<img src="../_pages/coronavirus/files/RMSD_result/SSGCID.png">

For RBD modeling, the RMSD between SARS-CoV-2 and SARS is 2.0072. The best performing GalaxyWEB model RMSD with SARS-CoV-2 is 0.1202 and the worst being 0.1526.

<img src="../_pages/coronavirus/files/RMSD_result/Galaxy.png">

For single chain modeling, the RMSD between SARS-CoV-2 and SARS is 10.936. The best performing Robetta model RMSD with SARS-CoV-2 is 2.5852 and the worst being 12.0975.

<img src="../_pages/coronavirus/files/RMSD_result/Robetta.png">

Looking at the RMSD values, SSGCID models far outperformed the models produced by SWISS. Although this may be due to a number of factors (e.g. different algorithms), one main factor is that the SSGCID modesl took much more computational power and time, which supports a positive correlation between computational power and accuracy. The difference between the best and worst GalaxyWEB models and high RSMD values between predicted models (e.g. 29.7861 between SSGCID_1 and SSGCID_4), indicate the potential of large variability between produced models. Lastly, there appears to be a negative correlation between sequence length and prediction accuracy for protein predictions of similar compuational power, where RBD models performed the best, followed by single chain models, and whole Spike models (SWISS) performing the worst.

To see the full RMSD report with RMSD values between the predicted models, download the results <a href="/multiscale_biological_modeling/_pages/coronavirus/files/RMSD_result/Module3RMSD_Result.csv" download>here</a>.

## More on RMSD

To use RMSD as a quantitative measure for comparing protein structures, the structures must first be superposed in such a way that the RMSD is minimized.

Back in the tutorial, superposing was accomplished by utilizing the *calcTransformation()* function, which returns the optimal transformation matrix between two structures such that the RMSD is minimized. This transformation matrix is consists of translation vector and rotation matrix, which can be calculated using the Kabsch Algorithm.

The source code for *calcTransformation()* can be found 
<a href="http://prody.csb.pitt.edu/_modules/prody/measure/transform.html#calcTransformation" target="_blank">here</a>.

### How it Works: Kabsch Algorithm (Partial Procrustes Superimposition)

The Kabsch Algorithm is an algorithm that finds the optimal rotation matrix in which the RMSD between two paired sets of points is minimized (the two sets must have the same number of points). In our case, the two sets of points are the 3D coordinate points of the Cα (carbon skeleton) of the two protein structures that we want to compare. The algorithm can be broken down into three major steps: Translation, Covariance, and Singular Value Decomposition.

#### Input
The input will be a (N x 3) matrix for each set of points, where N is the number of points per set. The three column represent the 3D coordinate set per N points.

#### Translation Step
Each set of points is translated such that their centroid lies on the origin of the coordinate system. This is easily done by subtracting the coordinates of the centroid from the respective point coordinates.

#### Covariance Step
The next step is to calculate the cross-covariance matrix. Let H be the cross-covariance matrix, and P and Q be the two translated input matrixes such that for the result of the algorithm, P will be rotated into Q.

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;H&space;=&space;P^{T}Q" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;H&space;=&space;P^{T}Q" title="\large H = P^{T}Q" /></a>

Or in summation notation:

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;H_{i,j}&space;=&space;\sum_{N}^{k=1}&space;P_{k,i}&space;Q_{k,j}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;H_{i,j}&space;=&space;\sum_{N}^{k=1}&space;P_{k,i}&space;Q_{k,j}" title="\large H_{i,j} = \sum_{N}^{k=1} P_{k,i} Q_{k,j}" /></a>

#### Singluar Value Decomposition (SVD) Step
It is possible to get the optimal rotation matrix, R, with the formula:

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;R&space;=&space;(H^TH)^{\frac{1}{2}}H^{-1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;R&space;=&space;(H^TH)^{\frac{1}{2}}H^{-1}" title="\large R = (H^TH)^{\frac{1}{2}}H^{-1}" /></a>

However, this is not always possible and can become quite complicated (e.g. H not having an inverse). Another method is to use singular value decomposition of the covariance matrix. Kabsch algorith utilizes SVD of H to compute R:

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;H&space;=&space;VSW^T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;H&space;=&space;VSW^T" title="\large H = VSW^T" /></a>

In order to ensure that the rotation matrix is a right-handed coordinate system, the matrix may need to be corrected by calculating the determinant of the dot product of W and V<sup>T</sup>:

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;d&space;=&space;sign(det(WV^T))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;d&space;=&space;sign(det(WV^T))" title="\large d = sign(det(WV^T))" /></a>

Finally, R can be calculated with the following matrix formula:

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;R&space;=&space;W\bigl(\begin{smallmatrix}&space;1&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1&space;&&space;0\\&space;0&space;&&space;0&space;&&space;d&space;\end{smallmatrix}\bigr)&space;V^T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;R&space;=&space;W\bigl(\begin{smallmatrix}&space;1&space;&&space;0&space;&&space;0\\&space;0&space;&&space;1&space;&&space;0\\&space;0&space;&&space;0&space;&&space;d&space;\end{smallmatrix}\bigr)&space;V^T" title="\large R = W\bigl(\begin{smallmatrix} 1 & 0 & 0\\ 0 & 1 & 0\\ 0 & 0 & d \end{smallmatrix}\bigr) V^T" /></a>

[Return to main text](accuracy){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
