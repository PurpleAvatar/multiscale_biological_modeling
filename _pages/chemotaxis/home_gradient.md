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

* SHUANGER: in the below, you have a parameter k_add. This parameter should be defined in the main text and it should be precisely defined as to what it is.  You passed this to parentheses but we should say exactly how the concentration of L, [*L*], is changing over time.

When traveling up the gradient with `k_add = 0.1`(d[L]/dt = 0.1[L] = 1000e<sup>0.1t</sup>, the cells demonstrated a continuous decrease in tumbling frequency until all receptors are saturated. Then the tumbling frequency is restored to the original, by a balance of increased ligand-receptor binding, and increased methylation states.

![image-center](../assets/images/chemotaxis_tutorial_addition01.png){: .align-center}

And a similar trend is observed with other gradients we've tried (gradients reflected by the rate of the fake ligand addition reaction). The slower the rate of ligand increases, the slower receptor binding increases, and the more moderate CheY-P drop becomes. Then the CheY-P is restored.

![image-center](../assets/images/chemotaxis_tutorial_addition03.png){: .align-center}

In the end, the high abundances of ligands make all receptors satruate, so that the cells no longer see any gradient, and they adapt to the higher concentration by restoring CheY-P to the original concentration. Despite the differences in the steepness of the gradient and the final concentration of the system, the model demonstrated robustness.

## Reversing the attractant gradient

Does the same robustness apply for the opposite direction - when the cell moves down the gradient? We care about down the gradient because cells aren't always in luck. When they are traveling in a direction with decreasing concentration, the cells should 1) be able to keep increasing tumbling frequency when moving along the wrong direction; 2) restore the background tumbling frequency when all ligands are removed - which also implies that methylation states should be restored (question for you: why?).

To simulate that, we will start from the steady state conditions for a cell in an area with high concentration (the cell has returned to background tumbling frequency, has high ligand binding and high methylation states), and allows the cell to experience decreasing concentration. If the system still demonstrate robustness, we should be able to see 1) CheY activities keep increasing until reaching a peak; 2) restoration of tumbling frequency and methylation states to background levels.

[Visit Ligand Removal Tutoiral](tutorial_removal){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

## Steady-state tumbling frequency remains robust

We should observe the increase in CheY-P followed by restoration of CheY-P. This is consistent with experimental observations[^Krembel2015]. We should also observe that `TA, TB, TC` restore to the original state of `adaptation.bngl`.

![image-center](../assets/images/chemotaxis_tutorial_removal01.png){: .align-center}

Like in the up-graident model, similar trend should be observed for different gradient shapes (reflected by the rate of the fake ligand removal reaction). The faster the ligands are removed, the faster CheY activities increase and the higher the peaks reach. Then all the tumbling frequencies are restored to the background level.

![image-center](../assets/images/chemotaxis_tutorial_removal02.png){: .align-center}


[Conclusion](home_conclusion){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^Krembel2015]: Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)
