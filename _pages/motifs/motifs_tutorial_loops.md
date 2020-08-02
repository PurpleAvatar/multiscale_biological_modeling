---
permalink: /motifs/tutorial_loops
title: "Looking for Loops in Transcription Factor Networks"
sidebar:
 nav: "motifs"
toc: true
toc_sticky: true
---

Let's take another look at that *E. coli* network, file can be downloaded here:
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/network_tf_tf_clean.txt" download="network_tf_tf_clean.txt">E. coli Network</a>

For the full Jupyter Notebook below, download here:
<a href="https://purpleavatar.github.io/multiscale_biological_modeling/downloads/Network_Demo.ipynb" download="Network_Demo.ipynb">Jupyter Notebook</a>

There are a few packages which need to be installed, here's list
1. this
2. this

We can import the network and see how many nodes and edges there are, additionally can see number of self-loops are present.

~~~ python
from network_loader import *
import random

txt_file = 'network_tf_tf_clean.txt'

network, vertex_names = open_network(txt_file)

# how many nodes & edges
print("Number of nodes: ", len(network.vs))
print("Number of edges: ", len(network.es))
print("Number of self-loops: ", sum(Graph.is_loop(network)))
~~~

* Number of nodes:  197
* Number of edges:  477
* Number of self-loops:  130

We can also create a visualization of the graph, shown here:

~~~ python
plot(network, vertex_label=vertex_names, vertex_label_size=8,
     edge_arrow_width=1, edge_arrow_size=0.5, autocurve=True)
~~~

![image-center](../assets/images/motifs_finding_ecoli_2.png){: .align-center}

We can create a random graph and visualize it here:

~~~ python
random.seed(42)
g = Graph.Erdos_Renyi(197,m=477,directed=True, loops=True)
plot(g, edge_arrow_width=1, edge_arrow_size=0.5, autocurve=True)
~~~

![image-center](../assets/images/motifs_finding_random.png){: .align-center}

We can investigate how many nodes and edges and self-loops

~~~ python
# how many nodes & edges
print("Number of nodes: ", len(g.vs))
print("Number of edges: ", len(g.es))
print("Number of self-loops: ", sum(Graph.is_loop(g)))
~~~

* Number of nodes:  197
* Number of edges:  477
* Number of self-loops:  5

And ta-da, the number of self-loops is significantly lower.

[Return to main text](finding#negative-vs-positive-autoregulation){: .btn .btn--primary .btn--large}{: style="font-size: 100%; text-align: center;"}
