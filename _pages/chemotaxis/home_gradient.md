---
permalink: /chemotaxis/home_gradient
title: "Modeling the gradient"
sidebar:
 nav: "chemotaxis"
---

## Up Gradient

In the Adaptation section, we modeled that 1) tumbling frequency decreases more when more ligand are added; 2) the cell can adapt to the current concentration. We only had an instantaneous change in concentration there. What we do not know yet is whether this instantaneous response can allow the cell to move along a continuous  **gradient**.

Our questions are, 1) Does the fast response allow the cell to constantly decrease its tumbling frequency when moving up a gradient? If the decrease in tumbling frequency only occurs once instead of happening continuously, then the cell won't be able to travel along the gradient, recall the cells are tiny. 2) Once the cell reaches a nutrient-rich region, can it still restore its tumbling frequency like it did when concentration was changed instantaneously? In another word, is the system still robust? If not, then the cell can't find its next meal.

In the adaptation model, we showed that the cells can respond and are robust to one perturbation in the environment. In this section, we would like to show the cells can respond and are robust to a series of perturbation.

[Visit Traveling Up Gradient Tutoiral](tutorial_gradient){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

When traveling up the gradient with `k_add = 0.1`(d[L]/dt = 0.1[L] = 1000e<sup>0.1t</sup>, the cells demonstrated a continuous decrease in tumbling frequency until all receptors are saturated. Then the tumbling frequency is restored to the original, by a balance of increased ligand-receptor binding, and increased methylation states. 

![image-center](../assets/images/chemotaxis_tutorial_addition01.png){: .align-center}

And a similar trend is observed with other gradients we've tried (gradients reflected by the rate of the fake ligand addition reaction). The slower the rate of ligand increasing, the slower receptor binding increases, and the more moderate CheY-P drop becomes. Then the CheY-P is restored.

![image-center](../assets/images/chemotaxis_tutorial_addition03.png){: .align-center}

In the end, the high abundances of ligand make all receptors satruate, so that the cells no longer see any gradient, and they adapt to the higher concentration by restoring CheY-P to the original concentration. Despite the differences in the steepness of the gradient and the final concentration of the system, the model demonstrated robustness.

## Down Gradient

Does the same robustness apply for the opposite direction - when the cell moves down the gradient? We care about down the gradient because cells aren't always in luck. When they are traveling in a direction with decreased concentration, the cells should 1) be able to keep increasing tumbling frequency when moving along the wrong direction; 2) restore the background tumbling frequency when all ligands are removed - which also implies that methylation states should be restored (question for you: why?).

To simulate that, we will start from the steady state conditions for a cell in an area with high concentration (the cell has returned to background tumbling frequency, has high ligand binding and high methylation states), and allows the cell to experience decreasing concentration. If the system still demonstrate robustness, we should be able to see 1) CheY activities keep increasing until reaching a peak; 2) restoration of tumbling frequency and methylation states to background levels.

[Visit Ligand Removal Tutoiral](tutorial_removal){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

We should observe the increase in CheY-P followed by restoration of CheY-P. This is consitent with experimental observations[^Krembel2015]. We should also observe that `TA, TB, TC` restores to the original state of `adaptation.bngl`.

![image-center](../assets/images/chemotaxis_tutorial_removal01.png){: .align-center}

Like in the up-graident model, similar trend should be observed for different gradient shapes (reflected by the rate of the fake ligand removal reaction). The faster the ligands are removed, CheY activities increas faster and reach higher peaks. Then all the tumbling frequencies are restored to the background level.

![image-center](../assets/images/chemotaxis_tutorial_removal02.png){: .align-center}


[Conclusion](home_conclusion){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}

[^Krembel2015]: Krembel A., Colin R., Sourijik V. 2015. Importance of multiple methylation sites in *Escherichia coli* chemotaxis. [Available online](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0145582)
