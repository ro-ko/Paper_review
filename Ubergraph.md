# "Ubergraphs: A Definition of a Recursive Hypergraph Structure"


[Paper Link](https://arxiv.org/abs/1704.05547)

</br>

### Table of Contents
0. [Introduction](#introduction)
0. [Related Work](#relatedWork)
0. [Method](#method)
0. [Conclusion](#conclusion)
0. [Summary](#summary)



</br>

## Introduction
- Formalize a recursive hypergraph data structure $\rightarrow$ ubergraph
- Graph $\in$ Hypergraph $\in$ Ubergraph
- Ubergraph allows edges to contain other edges as vertices

</br>

## Hypergraphs
- Generalization of a graph in which an edge can connect any number of vertices
- Hypergraph $H$ $(V,E)$ / $V$ : a set of vertices, $E$ : a set of hyperedges
- Incidence matrix of H is a matrix, $H_{ij}=\left\{\begin{matrix} 1 \; if \; v_i \in e_j\\0 \; otherwise\end{matrix}\right.$
- Levi graph is the bipartite graph G = $(V \cup E, E')$, where $(v_i,e_j) \in E' \; iff \; v_i \in e_j$

</br>

## Ubergraph
- One way to gerneralize hypergraphs is to allow edges to contain not only vertices but other edges
- For a finite set $X$, we define $P(X)^k = P(\bigcup_{i=0}^{k}P_i), P_0=X,\; P_i=P(\bigcup_{j=0}^{i-1}P_j) \; for \; i \geq 1$
- A depth k ubergraph U is a pair $(V,E)$ / $V$ : a set of vertices $E \subseteq P(V)^k$
    - Every hypergraph is a depth 0 ubergraph
- Ubergraph can be represented uber-Levi graph representation, incidence matrix $H_{(V+E),E}$
- Two vertices x,y of an ubergraph are adjacent if there is an uberedge which contains both elements
- Let $x,y ∈ V ∪ E$.A path P from x to y is a sequence
- Two ubergraph are isomorphic iff their uber-Levi graphs are isomorphic

</br>


## Summary
- Ubergraphs are a generalization of hypergraphs, hence many of the defini- tions of hypergraphs carry verbatim to ubergraphs

