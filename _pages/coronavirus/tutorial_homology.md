---
permalink: /coronavirus/tutorial_homology
title: "Protein Structure Prediction"
sidebar: 
 nav: "coronavirus"
toc: true
toc_sticky: true
---

Three protein prediction software, SWISS-MODEL, GalaxyWEB, and Robetta were chosen for template-based modeling of the SARS-CoV-2 S protein. Recall that the S protein is a homotrimer, meaning that it consists of three identical protein sturctures, or chains. Therefore, we will use the sequence of a single chain for modeling.

## SWISS-MODEL
<a href="https://swissmodel.expasy.org/" target="_blank">SWISS-MODEL</a> is a well-known structural bioinformatics web-server that specializes in homology modeling. The pipeline is comprised for four steps. 1) Using BLAST and HHblits, templates are identified and stored in the SWISS-MODEL Template Library. 2) The target sequence and template structure(s) are aligned. 3) Building the predicted models through a rigid fragment assembly approach. 4) Qualitiative Model Energy Analysis (QMEAN), a composite scoring function for model quality assessment.

First, download the sequence of the chain: <a href="/multiscale_biological_modeling/_pages/coronavirus/files/CoV2SpikeProteinSeq.txt" download>SARS-CoV-2 S Chain Sequence</a>

Next, head over to main page of <a href="https://swissmodel.expasy.org/" target="_blank">SWISS-MODEL</a> and click on *Start Modelling*.

<img src="../_pages/coronavirus/files/HomologyTutorial/SWISS1.png">

In the next page, copy and paste the sequence into the *Target Sequence(s):* box. Give the project a name and enter an email address to get a notification of when your results are ready. Finally, click on *Build Model*.

<img src="../_pages/coronavirus/files/HomologyTutorial/SWISS2.png">

Your results may take from an hour to a day depending on how busy the server is. Once you get an email notification saying that your model is ready, follow the link and you can download the models. Our results that we ran previously can also be downloaded below.

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/SWISS_Model.zip" download>SWISS-MODEL Results</a>

## Robetta
<a href="https://robetta.bakerlab.org/" target="_blank">Robetta</a> is a web-server that provides comparative and *ab initio* modeling of protein domains by utilizing the Rosetta fragment insertion method and de novo protocols. It allows for custom sequence alignments and can model multi-chain complexes. Robetta was chosen to model a single chain of the SARS-CoV-2 Spike protein. We will also be modeling a single chain of the SARS-CoV-2 S protein here.

First, if you had not already done so, download the sequence of the chain: <a href="/multiscale_biological_modeling/_pages/coronavirus/files/CoV2SpikeProteinSeq.txt" download>SARS-CoV-2 S Chain Sequence</a>

Go to <a href="https://robetta.bakerlab.org/" target="_blank">Robetta</a> and register for an account.

<img src="../_pages/coronavirus/files/HomologyTutorial/Robetta1.png">

After you are done, go to *Structure Prediction>Submit*.

<img src="../_pages/coronavirus/files/HomologyTutorial/Robetta2.png">

Create a name for the job, i.e. "SARS-CoV-2 Spike Chain". Copy and paste the sequence into the *Protein sequence* box. Check *CM only* (for comparative/homology modeling), complete the simple arithmetic problem and finally click *Submit*. Your results may take between an hour to a day. You will get an email notification after the job is complete, and you will be able to download the results. You can also download our results below.

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/Robetta_Model.zip" download>Robetta Results</a>

## GalaxyWEB
<a href="http://galaxy.seoklab.org/" target="_blank">GalaxyWEB</a> is a web-server with many available services including protein structure prediction, structure refinement, protein interaction prediction, and GPCR applications. GalaxyTBM (the template-based modeling service) uses *<a href="https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-019-3019-7" target="_blank">HHsearch</a>* to identify up to 20 templates, then matches the core sequence with the templates using *<a href="http://prodata.swmed.edu/promals3d/info/promals3d_help.html" target="_blank">PROMALS3D</a>*. Next, models are generated using *<a href="https://pubmed.ncbi.nlm.nih.gov/19089941/" target="_blank">MODELLERCSA</a>.

Because GalaxyWEB as a sequence limit of 1000 amino acids, we cannot use the S protein chain. Instead, we can model the Receptor Binding Domain (RBD) of the S protein instead.

First, download sequence: 
<a href="/multiscale_biological_modeling/_pages/coronavirus/files/CoV2SpikeRBDSeq.txt" download>CoV-2 RBD Sequence</a>

Go to <a href="http://galaxy.seoklab.org/" target="_blank">GalaxyWEB</a>. At the top, go to *Services>TBM*.

<img src="../_pages/coronavirus/files/HomologyTutorial/Galaxy1.png">

Enter a job name, i.e. SARS-CoV-2 RBD. Enter an email address and then copy and paste the sequence into the *SEQUENCE* box. Finally, click submit.

<img src="../_pages/coronavirus/files/HomologyTutorial/Galaxy2.png">

Your results will be done within a day and you will recieve an email notification. Then, you will be able to download your results. You can also download our results below.

<a href="/multiscale_biological_modeling/_pages/coronavirus/files/GalaxyWEB_Models.zip" download> GalaxyWEB Results </a>

<hr>

In the next section and tutorial, we will learn how to assess predicted models and see how accurate our results were.


[Return to main text](homology){: .btn .btn--primary .btn--x-large}
{: style="font-size: 100%; text-align: center;"}


