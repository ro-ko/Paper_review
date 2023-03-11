# Variational Inference: A Review for Statisticians


[Paper Link](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b8b624f3-19ad-46bc-a708-9655a8c1a558/BleiKucukelbirMcAuliffe2017.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230310%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230310T082106Z&X-Amz-Expires=86400&X-Amz-Signature=d23976072aaf60216f5d1fb29328fc19668bfebfe5c65e156aa75ba6b9fa27f8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22BleiKucukelbirMcAuliffe2017.pdf%22&x-id=GetObject)  

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

- difficult-to-compute probability densities
- VI approximates probability densities through optimization
-  VI tends to be faster than classical methods, such as Markov chain Monte Carlo sampling
- posit a family of densities and find a member of that family
- Closeness is measured by Kullback–Leibler divergence
- mean-field variational inference

</br>

## Introduction
Variational inference is used to **approximate posterior densities for Bayesian models**, an alternative strategy to MCMC sampling and tends to be faster and easier to scale to large data.  
But it is studied less rigorously than MCMC, and its statistical properties are less well understood.  

Consider a joint density of latent variables $z = z_{1:m}$ and observations $X = x_{1:n}$  
$p(z,X) = p(z)p(X|z)$  

In MCMC, approximate the posterior with an empirical estimate constructed from the collected samples.  

Landmark developments include the Metropolis–Hastings algorithm (Metropolis et al. 1953; Hastings 1970), the Gibbs sampler (Geman and Geman 1984), and its application to Bayesian statistics (Gelfand and Smith 1990).  

Rather than use sampling, the main idea behind variational inference is to use optimization.  
1. posit a family of approximate densities Q
2. minimizes the Kullback-Leibler (KL) divergence to the exact posterior  

$q^*(z) = \underset{q(z)\in Q}{argmin} KL(q(z)||p(z|x))$  

One of the key ideas behind variational inference is to choose Q to be flexible enough to capture a density close to p(z | x), but simple enough for efficient optimization.  

When should a statistician use MCMC and when should she use variational inference?

### MCMC
- tend to be more computationally intensive
- provide guarantees of producing (asymptotically) exact samples from the target density  

### VI
- only find a density close to the target
- tends to be faster than MCMC
- takes advantage of methods like stochastic optimization  

Thus, variational inference is suited to large datasets and scenarios. MCMC is suited to smaller datasets and scenarios  

Another factor is the geometry of the posterior distribution.

For example, the posterior of a mixture model has multiple modes. If the model permits Gibbs sampling is a powerful approach to sampling. But for some mixture model Gibbs is not the option, VI may perform better than a more general MCMC technique.  
[Gibbs sampling](https://ratsgo.github.io/statistics/2017/05/31/gibbs/)

VI underestimates the variance of the posterior density.  
MCMC is a tool for simulating from densities and variational inference is a tool for approximating densities.  

variational inference: mean-field inference and coordinate-ascent optimization.  

The goal of variational inference is to approximate a conditional density of latent variables given observed variables.  

### Bayesian mixture of Gaussians  
Consider  a Bayesian mixture of unit-variance univariate Gaussians with K mixture components.  

$\mu_k ~ N(0,\sigma^2),k=1,\cdots,K$  
$c_i ~ catgorical(1/K,\cdots,1/K),i=1,\cdots,n$  
$x_i | c_i ,\mu~N(c_i^T\mu,1),i=1,\cdots,n$  

$p(x)=\sum_c{p(c)}\int p(\mu)\prod_{j=1}^n p(x_i|c_i,\mu)d\mu$

Intracttable!! $O(K^n)$  

### ELBO
$q^*(z) = \underset{q(z)\in Q}{argmin} KL(q(z)||p(z|x))$  
$KL(q(z)||p(z|x))=E[log q(z)]-E[log p(z,x)]+log p(x)$  
$ELBO(q)=E[log p(z,x)]-E[log q(z)]$  
$log p(x) = KL(q(z)||p(z|x))+ELBO(q)$  

KL is non-negative by Jensen's inequality.  
ELBO has led to using to the variational bound as a model selection criterion.  

ELBO is the expected complete log-likelihood, which is optimized by the EM algorithm.  
EM assumes the expectation under p(z | x) is computable and uses it in otherwise difficult parameter estimation problems.  
But VI do not.  

### mean-field variational family  

the latent variables are mutually independent and each governed by a distinct factor in the variational density.  
$q(z)=\prod_{j=1}^m q_j(z_j)$  

 The data x does not appear in Equation. Instead, it is the ELBO, and the corresponding KL minimization problem. Structured and mixture-based variational families come with a more difficult-to-solve variational optimization problem.  

<center>
<img
    src="image/VI/Fig_1.png"
    width="50%"
/>
</center>

 ### coordinate ascent variational inference (CAVI)  

 CAVI iteratively optimizes each factor of the mean-field variational density, while holding the others fixed.  

 $q_j^*(z_j) \propto exp\{E_{-j}[log p(z_j|z_{-j},x)]\}$
 $q_j^*(z_j) \propto exp\{E_{-j}[log p(z_j,z_{-j},x)]\}$ by mean-field property  

- CAVI can also be seen as a “message passing” algorithm.  
- CAVI is closely related to Gibbs sampling   

$ELBO(q_j)=E_j[E_{-j}[log p(z_j,z_{-j},x)]]-E_j[log q_j(z_j)]+const$  
It means negative KLD betwwen $q_j(z_j), q_j^*(z_j)$

<center>
<img
    src="image/VI/Fig_2.png"
    width="50%"
/>
</center>

</br>
Each initialization reaches a different value.  
In terms of KL(q||p), better local optima give variational densities that are closer to the exact posterior. This is not always a disadvantage.  

Why? 
- Representing one of these modes is sufficient for exploring latent clusters or predicting new observations.  

Assess convergence  
- Monitoring the ELBO in CAVI is simple; we typically declare convergence once the change in ELBO falls below some small threshold.  
- Suggest computing the average log predictive of a small held out dataset.  

Numerical stablity  
- Probabilities are constrained to live within [0, 1]. 
- $log[\sum_i exp(x_i) = \alpha + log[\sum_i exp(x_i-\alpha)]]$  

<center>
<img
    src="image/VI/Fig_3.png"
    width="50%"
/>
</center>

### Stochastic Variational Inference (SVI)

The coordinate ascent structure of the algorithm requires iterating through the entire dataset at each iteration.  

An alternative to coordinate ascent is **gradient-based optimization**  

Repeat
1. subsamples a data point from the full dataset
2. uses the current global parameters to compute the optimal local parameters for the subsampled data point
3. adjusts the current global parameters in an appropriate way.  

How it works?  
In gradient-based optimization, the natural gradient accounts for the geometric structure of probability parameters.  

In exponential families, the natural gradient is the inverse Riemannian metric and the inverse Fisher information matrix.  

$∇λELBO = a'' (λ)(Eφ[αˆ] − λ)$
$g(λ) = Eφ[αˆ] − λ$  

A gradient-based optimization algorithm.
$λ_t =λ_{t−1}+ε_t g(λ_t)$
$λ_t =(1−ε_t)λ_{t−1} +ε_t Eφ[αˆ]$  

Stochastic optimization algorithms follow noisy but cheap-to-compute gradients to reach the optimum of an objective function.  


## Related Work
- Posterior estimates of the topics and topic proportions can be used to summarize, visualize, explore, and form predictions about the documents.
- One motivation for topic modeling is to get a handle on massive collections of documents.
- With SVI, topic models scale up to millions of documents.

<center>
<img
    src="image/VI/Fig_4.png"
    width="50%"
/>
</center>

</br>

## Conclusion
- Paper described variational inference, a method that uses optimization to make probabilistic computations. 
- Then described the mean-field family, that is, the family of fully factorized densities of the latent variables.

</br>

## Open Problems
- To develop variational inference methods that optimize other measures.
  - Developed divergences based on lower bounds that are tighter than the ELBO
  -  α-divergence measures.
- To develop better approximations while maintaining efficient optimization.
  - structured variational inference.
  - generic structured variational inference in a stochastic optimization algorithm.
  - Gaussian variational families with nondiagonal covariance.
  - post-processed the mean-field parameters to correct for underestimating the variance.
- Interface between variational inference and MCMC
- The statistical properties of variational inference are not yet well understood