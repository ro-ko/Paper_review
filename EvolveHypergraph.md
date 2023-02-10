# "EvolveGraph: Multi-Agent Trajectory Prediction with Dynamic Relational Reasoning "

[Paper Link](https://arxiv.org/abs/2208.05470)  
[NBA Dataset Link](https://github.com/linouk23/NBA-Player-Movements)

</br>

### Table of Contents
0. [Abstract](#abstract)
0. [Introduction](#introduction)
0. [Related Work](#relatedWork)
0. [Method](#method)
0. [Conclusion](#conclusion)
0. [Summary](#summary)

</br>

## Abstract

- propose a group-aware relational reasoning approach (named EvolveHypergraph)
- Use dynamically evolving relational structures
- connect multiple nodes to enable group-aware relational reasoning in an unsupervised manner
- regularize the smoothness of the relation evolution and the sparsity of the inferred graphs or hypergraphs
- achieves state-of-the-art performance in long-term prediction.

</br>

## Introduction
- only the historical state information is available in trajectory prediction, which makes group recognition much more difficult
- Group-LSTM [16] uses the coherent filtering technique
    - Using social pooling layer (fixed in the whole prediction horizon and difficult to explain)
- propose to infer the hypergraph topology in a data-driven manner
- main contributions
    1. propose a group-aware relational reasoning approach
    2. propose effective mechanisms to regularize the smoothness
    3. validate the proposed model on both crowd simulations and trajectory prediction benchmarks

</br>

## Related Work
- Traditional approaches
    - physics-based models
    - heuristics-based models
    - probabilistic graphical models
- The relational learning and reasoning module is a crucial component in multi-agent trajectory prediction

</br>

## Method
agents' trajectories as $X_{1:T}=\{X_{1:T}^i,T=T_h+T_f,i=1, \cdots ,N\}$ where $N$ represents the number of involved agents, $T_h$ : history, $T_f$ : future.  
$X_t^i=(x_t^i,y_t^i)$ as agent i, 2D coordinate at t.  

The object of probabilistic trajectory prediction is the conditonal distribution $p(X_{T_h+1:T_h+T_f}|X_{1:T_h})$  

EvolveHypergraph, an encoder-decoder architecture with iterative sliding window to enable dynamic relationa;l reasoning for long-term prediction.

### **Encoder**
- infer relation graphs and hypergraphs
- latent space based on historical state observations  

Fisrt round  
$v_i^{self}=f_h(X_{t-T_h+1:t}^i)$  
$e_{CG,ij}^1=f_{CG,e}^1([v_i^{self},v_j^{self}])$  
$v_i^{social}=f_{CG,v}^1(\underset{i \neq j}{\sum}e^1_{CG,ij})$  

Second round  
$V^1_{CG,i}=[V_i^{self},V_i^{social}]$  
$e_{CG,ij}^2=f_{CG,e}^2([v_{CG,i}^1,v_{CG,j}^1])$  
  
Compute hyperedge features  
$I_{PIM}=f_{PIM}(V_{CG}^1)(f_{PIM}(\cdot):MLP) + Gumbel-softmax \; distribution \rightarrow I_{HG}=f_{im}(V_{CG}^1):=Gumbel-softmax(I_{PIM})$  

Need to set the maximum number of hyperedges denoted by M according to specific applications.

$G_{obs}=\{V_{obs},E_{obs}\}$  
$V_{obs}=\{v_i, i \in \{ 1,\cdots,N \} \}$  
$E_{obs}=\{e_{ij},i,j \in \{1,\cdots,N\}\}$

$e_{ij}$ is directed edge from node j to i.  
Agent has two types of attributes: a self-attribute, a social-attribute.

$e_{HG,m}^1=f_{HG,e}^1(\underset{i \in H_m}{\sum}V_{CG,i}^1)$  
$V_{HG,m}^1=f_{HG,v}^1(\underset{m:i \in H_m}{\sum}e_{HG,m}^1)$  
$e_{HG,m}^2=f_{HG,e}^2(\underset{i \in H_m}{\sum}V_{HG,i}^1)$  

Inferring relation patterns  
$z_{CG,ij}=Softmax((e_{CG,ij}^2+g)\tau),i,j\in\{1,\cdots N\}$  
$z_{HG,m}=Softmax((e_{HG,m}^2+g)\tau),m\in\{1,\cdots M\}$
$g$ denotes a vetcor of i.i.d smaples from the Gumbel(0,1), $\tau$ is temperature coefficient.

$z_{CG,ij}=[z_{CG,ij,1},\cdots,z_{CG,ij,L_{CG}}]$  
$z_{HG,m}=[z_{HG,m,1},\cdots,z_{HG,m,L_{HG}}]$  

$q_{CG}(z_{CG,\beta}|X_{t-T_h+1:t}),q_{HG}(z_{HG,\beta}|X_{t-T_h+1:t}) = Encoder(X_{t-T_h+1:t})$

### **Decoder**
- leverage latent relational structures to generate the distribution of future trajectory


</br>

## Conclusion
- 

</br>

## Summary
- 
