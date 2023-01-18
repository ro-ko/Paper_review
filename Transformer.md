# Paper title

[Paper Link]() \
[Github Link]()

</br>

### Table of Contents
0. [Abstract](##Abstract)
0. [Introduction](##Introduction)
0. [Related Work](##RelatedWork)
0. [Method](##Method)
0. [Conclusion](##Conclusion)
0. [Summary](##Summary)

</br>

## Abstract

- Sequence transduction models
- The best performing models connect the encoder and decoder through an attention mechanism
- Propose simple network based soley on attention mechanisms
- Parallelizable

</br>

## Introduction

- Traditional Recurrent models : critical at longer sequence lengths
- Recent work : factorization trick, conditional computation
- Fundamental constraint remains -> sequential computation

</br>

## Related Work

### - Self-attention(intra-attention)
### - End-to-end memory networks based on a recurrent attention mechanism

</br>

## Method

- Encoder-Decoder structure

### Encoder 
Input : sequence of symbol representation $(x_1,...,x_n)$

Output : sequence of continous representation $z = (z_1,...,z_n)$

### Decoder
Input : $z$

Output : Symbols one element at a time $(y_1,...,y_m)$
#
Both the encoder and decoder have stacked self-attention and point-wise, fully connected layers

<center>
<img
    src="image/Transformer/figure1.png"
    width="50%"
/>

Figure 1. model architecture
</center>

### Encoder
Identical layer : 6 \
Each layer : 2 sub-layers (multi-head self-attention mechanism, position wise fully connected feed-forward network) \
A residual connection each sub-layer : $LayerNorm(x+Sublayer(x))$

Output dimensions : 512

</br>

## Conclusion

- 

</br>

## Summary

- 
