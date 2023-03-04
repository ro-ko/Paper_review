# "Denoising Diffusion Probabilistic Models"

[Paper Link](https://arxiv.org/abs/2006.11239)  
[Github Link](https://github.com/hojonathanho/diffusion)

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

- diffusion probabilistic models
- admit a progressive lossy decompression scheme
- a weighted variational bound designed


</br>

## Introduction
- A diffusion probabilistic model is a parameterized Markov chain trained using variational inference to produce samples matching the data after finite time
- gradually adds noise to the data in the opposite direction of sampling until signal is destroyed
- denoising score matching over multiple noise levels
- Langevin dynamics during sampling
- 
</br>

## Related Work
- VAEs
- learning transition operators of Markov chains include infusion training, variational walkback, generative stochastic networks, and others

</br>

## Method
- The joint distribution $p_\theta (x_0:T)$ is called the reverse process, and it is defined as a Markov chain with learned Gaussian transitions starting at $p(x_T) = N(x_T ; 0, I)$
- posterior $q(x_1:T|x_0)$, called the forward process or diffusion process
- forward process admits sampling $x_t$ at an arbitrary timestep t in closed form

</br>

## Conclusion
- paper has found connections among diffusion models and variational inference for training Markov chains, denoising score matching and annealed Langevin dynamics (and energy-based models by extension), autoregressive models, and progressive lossy compression

</br>

## Summary
- 
