---
permalink: /chemotaxis/home_gradient
title: "Modeling the gradient"
sidebar:
 nav: "chemotaxis"
---

## Traveling up an attractant gradient

In the previous lesson, we saw that *E. coli* is able to adapt its default tumbling frequency to the current background concentration of attractant. To replicate this behavior using BioNetGen, we simulated an instantaneous increase in concentration from one stable concentration level to another.

Yet imagine a glucose cube in an aqueous solution. As the cube dissolves, there will be a **gradient** of decreasing glucose concentration that radiates outward from the cube, where this concentration is highest. How will the tumbling frequency of *E. coli* change if the bacterium is moving along a continuous gradient of attractant concentration?  Will the tumbling frequency decrease continuously as well, or will the methylation pathways mentioned in the previous lesson cause more complicated behavior?

Furthermore, once the cell reaches a region of high attractant concentration, will its default tumbling frequency stabilize to the same steady-state?  And how much does this steady-state tumbling frequency change as we alter the "steepness" of the attractant gradient (i.e., how quickly the attractant concentration increases)?

In the following tutorial, we will modify our model from the previous lesson by increasing the concentration of the attractant ligand at an exponential rate and seeing how the concentration of CheY changes. Moreover, we will examine how the concentration of CheY responds to a change in the rate at which attractant ligand is added.

[Visit tutorial](tutorial_gradient){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Steady-state tumbling frequency is robust when traveling up an attractant gradient

Recall that we used the expression [*L*] to denote the concentration of our ligand *L* and *l*<sub>0</sub> to denote the ligand's initial concentration. To represent exponential growth in the concentration of the ligand, we will have that [*L*] = *l*<sub>0</sub> · *e*<sup>*k* · t</sup>, where *t* is the time and *k* is a parameter dictating exponential growth; the higher the value of *k*, the faster the growth in the ligand concentration.

For example, the following figure depicts the concentration of phosphorylated CheY (highlighted in blue) over time when *l*<sub>0</sub> = 1000 and *k* = 0.1. The concentration of phosphorylated CheY (and therefore the tumbling frequency) initially decreases sharply as the ligand concentration increases, but after all ligands become bound to receptors (shown by the plateau in the red curve), the methylation of receptors causes the concentration of CheY to return to its equilibrium.

![image-center](../assets/images/chemotaxis_tutorial_addition01.png){: .align-center}

Our next question is what happens if we were to change *k*, the growth rate of the ligand concentration. The following figure plots only the concentration of CheY over time for multiple simulations in which we vary the growth parameter *k*. The faster the rate at which the concentration of the ligand increases, the faster the increase in receptor binding, and the steeper the drop in the concentration of phosphorylated CheY.

![image-center](../assets/images/chemotaxis_tutorial_addition03.png){: .align-center}

More importantly, note that regardless of the rate of increase in ligand concentration, the system is always able to return to the same equilibrium concentration of phosphorylated CheY.

## Reversing the attractant gradient

And what if a cell is moving away from an attractant, down a concentration gradient? We would hope that the cell would be able to *increase* its tumbling frequency in this case (i.e., increase the concentration of phosphorylated CheY), and then restore the background tumbling frequency after all ligands have become unbound by removing methylation.

To simulate this situation, we will model a cell starting with steady-state conditions in an area of high ligand concentration (i.e., the cell has high ligand binding and high methylation states). In this case, we want exponential *decay*, meaning that the ligand concentration is still given by the equation [*L*] = *l*<sub>0</sub> · *e*<sup>*k* · t</sup>, but *k* is negative.

**STOP:** What happens to the plot of [*L*] = *l*<sub>0</sub> · *e*<sup>*k* · t</sup> as *k* decreases if *k* is negative? How do you think the value of *k* will affect the concentration of phosphorylated CheY over time?
{: .notice--primary}

You may like to go it alone and modify the previous tutorial yourself to account for traveling down an attractant gradient. Otherwise, we will provide a separate tutorial for this case.

[Visit tutorial](tutorial_removal){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Steady-state tumbling frequency remains robust

The following figure shows the plot of different molecules in our model as the concentration of attractant ligand decreases exponentially with *l*<sub>0</sub> = 10<sup>7</sup> for *k* equal to 0.3. As we expected, the concentration of phosphorylated CheY spikes as bound ligands break free and there are not enough free ligands to replace them. After this spike, methylation of receptors causes the concentration of phosphorylated CheY to steadily return back to its equilibrium.

![image-center](../assets/images/chemotaxis_tutorial_removal01.png){: .align-center}

To adapt to a higher ligand concentration, the methlyation states of the cell become higher. If the cell then moves down the gradient to somewhere with no ligand present, the methylation states should also be restored. Check that the new steady state concentration of receptors at high, medium, and low methylation states match the starting concentration of our [adaptation simulation](tutorial_adap).

In the interest of due diligence, we will also test the robustness of the model to ascertain whether the CheY concentration will return to the same steady-state for a variety of values of *k*. As in the case of an increasing gradient, we see that the more sudden the change in the concentration of attractant, the sharper the spike, but that in each case, methylation does its work to bring the concentration back to the same steady-state. More importantly, these figures are consistent with experimental observations.[^Krembel2015]

![image-center](../assets/images/chemotaxis_tutorial_removal02.png){: .align-center}

## Connection to next section

* Note to self: need compelling connection to next section, which is that we have been operating under the assumption that if a bacterium senses a higher attractant gradient, then it should be able to decrease its tumbling frequency.  But its movements are *random* ... why is a decrease in tumbling frequency helpful to find the attractant?  There is no immediate intuitive answer to this question, but we will show in the next section how to provide a compelling explanation for why E. coli has evolved the way it has through the power of modeling.

[Next lesson](home_conclusion){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^Krembel2015]: Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)
