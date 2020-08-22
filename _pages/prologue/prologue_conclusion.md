---
permalink: /prologue/conclusion
title: "Conclusion"
sidebar:
 nav: "prologue"
 toc: true
 toc_sticky: true
---

## A reflection on Turing patterns

The Turing patterns that emerge from our animations in the previous section are a testament to the human eye's ability to find organization within the net behavior of tens of thousands of particles.  The patterns are unquestionably present, but they are also noisy --- even in the dark red regions we will have quite a few green particles, and vice-versa. The rapid inference of large-scale patterns from small-scale visual phenomena is one of the tasks that our brains have evolved to perform well.

This reaction-diffusion system is remarkable because it is so **fine-tuned**, meaning that that very slight changes in parameter values can lead to significant changes in the overall system. In the case of our model, these changes could convert spots to stripes, or they could influence how clearly defined the boundaries of the Turing patterns are.

Much later in this course, we will see an example of a biological system that is the opposite of fine-tuned. In such a **robust** system, variation in the parameters does not lead to substantive changes in the ultimate behavior of the system. Robust processes are vital for processes in which an organism needs to be resilient to small changes. We will say more about robustness later.

It turns out that although Turing's work offers a compelling argument for how zebras might have gotten their stripes, the exact mechanism by which these stripes form is still an unresolved question. Although zebras are still up in the air, the pigmentation of *zebrafish* does follow a Turing pattern because two types of pigment cells follow a reaction-diffusion model much like the one we presented above.

CITATION: https://www.pnas.org/content/106/21/8429.

We also have qualitative evidence that the pigmentary patterns arising in fish are due to a fine-tuned system. For example, note that following two photos of giant pufferfish. These fish are genetically very similar, but their skin patterns are very different, with one having spots and the other exhibiting a complex pattern of stripes. What seems like a drastic change in the appearance of the fish can actually be attributable to a small change of parameters in a fine-tuned system that is driven only by random interactions.

* NOAH: Insert table of pufferfish photos and cite -- https://www.123rf.com/photo_26775011_giant-puffer-fish.html and https://en.wikipedia.org/wiki/File:Giant_Puffer_fish_skin_pattern.JPG or equivalent quality


## Exercises

* Make a cell update an exercise at end.

* Good exercise on changing the diffusion rates outside of what is specified by Gray-Scott.

* Good questions below. May need to be exercises.

**STOP**: Is it ever possible for a square to have a concentration greater than 1? Why or why not?
{: .notice--primary}

**STOP**: Note that the concentrations of all of the particles add up to 1 in each step.
{: .notice--primary}

## Notes to selves

* Explain the colors used very carefully to tie them to concentrations, but only do so after we initially update them.

* In later iteration of this, we need to probably update the figures to show how things update.

* Note to add link to cellular automata and P4L. Should we explicitly call this an automaton? I think yes.

[Next chapter](../motifs/home){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}
