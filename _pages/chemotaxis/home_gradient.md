---
permalink: /chemotaxis/home_gradient
title: "Modeling a Bacterium's Response to an Attractant Gradient"
sidebar:
 nav: "chemotaxis"
---

## Traveling up an attractant gradient

In the previous lesson, we saw that *E. coli* is able to adapt its default tumbling frequency to the current background concentration of attractant. To replicate this behavior using BioNetGen, we simulated an instantaneous increase in concentration from one stable concentration level to another.

Yet imagine a glucose cube in an aqueous solution. As the cube dissolves, a **gradient** will form, with a decreasing glucose concentration that radiates outward from the cube. How will the tumbling frequency of *E. coli* change if the bacterium is moving up a gradient of increasing attractant concentration?  Will the tumbling frequency decrease continuously as well, or will the methylation pathways mentioned in the previous lesson cause more complicated behavior?

Furthermore, once the cell reaches a region of high attractant concentration, will its default tumbling frequency stabilize to the same steady-state?  And how much does this steady-state tumbling frequency change as we alter the "steepness" of the attractant gradient (i.e., how quickly the attractant concentration increases)?

In the following tutorial, we will modify our model from the previous lesson by increasing the concentration of the attractant ligand at an exponential rate and seeing how the concentration of phosphorylated CheY changes. Moreover, we will examine how this concentration changes as we change the gradient's "steepness", or the rate at which attractant ligand is increasing.

[Visit tutorial](tutorial_gradient){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Steady-state tumbling frequency is robust when traveling up an attractant gradient

Recall that we used the expression [*L*] to denote the concentration of ligand *L* and *l*<sub>0</sub> to denote the initial concentration of the ligand. To represent exponential growth in the concentration of the ligand, [*L*] = *l*<sub>0</sub> · *e*<sup>*k* · t</sup>, where *t* is the time since the start and *k* is a parameter dictating exponential growth; the higher the value of *k*, the faster the growth in the ligand concentration.

For example, the following figure depicts the concentration of phosphorylated CheY (highlighted in blue) over time when *l*<sub>0</sub> = 1000 and *k* = 0.1. The concentration of phosphorylated CheY (and therefore the tumbling frequency) initially decreases sharply as the ligand concentration increases, but after all ligands become bound to receptors (shown by the plateau in the red curve), the methylation of receptors causes the concentration of phosophorylated CheY to return to its equilibrium.

![image-center](../assets/images/chemotaxis_tutorial_addition01.png){: .align-center}

Our next question is what happens if we change *k*, the growth rate of the ligand concentration. The following figure shows the results of multiple simulations in which we vary the growth parameter *k* and plot the concentration of phosphorylated CheY over time. The larger the value of *k*, the faster the increase in receptor binding, and the steeper the drop in the concentration of phosphorylated CheY.

More importantly, note that this figure illustrates the *robustness* of our model to *k*, the growth in ligand concentration. For widely varying rates of increase in ligand concentration, the system is always able to return to approximately the same equilibrium concentration of phosphorylated CheY (and therefore the same background tumbling frequency).

![image-center](../assets/images/chemotaxis_tutorial_addition03.png){: .align-center}

## Reversing the attractant gradient

And what if a cell is moving away from an attractant, down a concentration gradient? We would hope that the cell would be able to *increase* its tumbling frequency in this case (i.e., increase the concentration of phosphorylated CheY), and then restore the background tumbling frequency by removing methylation.

To simulate this situation, we will model a cell in a high ligand concentration that is at steady-state, meaning that methylation is also elevated. In this case, we want the ligand concentration to *decay* exponentially, meaning that the ligand concentration is still given by the equation [*L*] = *l*<sub>0</sub> · *e*<sup>*k* · t</sup>, but *k* is negative.

**STOP:** If *k* is negative, what happens to the plot of [*L*] = *l*<sub>0</sub> · *e*<sup>*k* · t</sup> for decreasing values of *k*? How do you think the value of *k* will affect the concentration of phosphorylated CheY over time?
{: .notice--primary}

You may like to go it alone and modify the previous tutorial yourself to account for traveling down an attractant gradient. Otherwise, we will provide a separate tutorial for you to explore.

[Visit tutorial](tutorial_removal){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Steady-state tumbling frequency remains robust when traveling down an attractant gradient

The following figure shows the plot of molecules in our model as the concentration of attractant ligand decreases exponentially with *l*<sub>0</sub> = 10<sup>7</sup> and *k* equal to -0.3. As we expected, the concentration of phosphorylated CheY spikes as bound ligands break free and there are not enough free ligands to replace them. After this spike, methylation of receptors causes the concentration of phosphorylated CheY to steadily return back to its equilibrium. Note also in the figure below that the cell removes methylation as it moves down the gradient.

![image-center](../assets/images/chemotaxis_tutorial_removal01.png){: .align-center}

<!--
 In particular, the new steady methylation states  adapt to a higher ligand concentration, the methlyation states of the cell become higher. If the cell then moves down the gradient to somewhere with no ligand present, the methylation states should also be restored. Check that the new steady state concentration of receptors at high, medium, and low methylation states match the starting concentration of our [adaptation simulation](tutorial_adap).
-->

To be thorough, we should also test the robustness of our model to see whether the CheY concentration will return to the same steady-state for a variety of values of *k* when *k* is negative. As in the case of an increasing gradient, the figure below shows that the more sudden the change in the concentration of attractant, the sharper the spike. And yet regardless of the value of *k*, methylation does its work to bring the concentration back to the same steady-state. More importantly, this figure and the one above are confirmed by experimental observations.[^Krembel2015]

![image-center](../assets/images/chemotaxis_tutorial_removal02.png){: .align-center}

## Connection to next section

We hope that through exploring this module, you have gained an appreciation for the elegant mechanism of bacterial chemotaxis, as well as the power of rule-based modeling for simulating a complex biochemical system.

And yet throughout this discussion we have made one major omission. We have seen that *E. coli* goes to great lengths to ensure that if it detects a relative increase in concentration (i.e., an attractant gradient), then it can reduce its tumbling frequency in response. But what we have not explored is *why* this is a useful strategy.

After all, even though the tumbling frequency is tied to relative attractant concentration, the direction of the bacterium's move in any "run" step is random! So why would a decrease in tumbling frequency help  *E. coli* move toward an attractant?

This question has no immediate intuitive answer, but in this module's final lesson, we will apply modeling to explain why the random-walk algorithm that *E. coli* uses to explore its environment is in fact an extremely clever way of locating resources.

[Next lesson](home_conclusion){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^Krembel2015]: Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)
