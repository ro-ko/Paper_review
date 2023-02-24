# "On Calibration of Modern Neural Networks"

[Paper Link](https://arxiv.org/abs/1706.04599)  
[Github Link]()

</br>

### Table of Contents
0. [Abstract](#abstract)
0. [Introduction](#introduction)
0. [Definitions](#definitions)
0. [Miscalibration](#miscalibration)
0. [Methods](#methods)
0. [Results](#results)
0. [Summary](#summary)

</br>

## Abstract

- Confidence calibration
    -  the problem of predict- ing probability estimates representative of the true correctness likelihood
- Modern neural networks are poorly calibrated
- Depth, width, weight decay, and Batch Normalization are important factors influencing calibration
- recommend using temperature scaling

</br>

## Introduction

- The probability associated with the predicted class label should reflect its ground truth correctness likelihood
- mod- ern neural networks are no longer well-calibrated

<center>
<img
    src="image/Calibration/Fig1.png"
    width="50%"
/>

Figure 1. Confidence histograms (top) and reliability diagrams (bottom) for a 5-layer LeNet (left) and a 110-layer ResNet (right) on CIFAR-100
</center>

Paper's goal is not only to understand why neural networks have become miscalibrated, but also to identify what methods can alleviate this problem  
find that a single-parameter variant of Platt scaling which we refer to as temperature scaling is often the most effective method at obtaining calibrated probabilities

</br>

## Definitions

- Reliability Diagrams
- Expected Calibration Error (ECE)

<center>
<img
    src="image/Calibration/Fig2.png"
    width="50%"
/>

Figure 2. The effect of network depth (far left), width (middle left), Batch Normalization (middle right), and weight decay (far right) on miscalibration, as measured by ECE (lower is better)
</center>
</br>

- Maximum Calibration Error (MCE)
- Negative log likelihood

## Miscalibration
- Model capacity  
- Batch Normalization
- Weight decay
- NLL


</br>

## Methods
- Histogram binning
- Isotonic regression
- Bayesian Binning into Quantiles (BBQ)
- Platt scaling (temperature)
<center>
<img
    src="image/Calibration/Fig3.png"
    width="50%"
/>

Table 1. ECE (%) (with M = 15 bins) on standard vision and NLP datasets before calibration and with various calibration methods. The number following a model’s name denotes the network depth
</center>

</br>

## Results
- Temperature scaling outperforms all other methods on the vision tasks, and performs comparably to other methods on the NLP datasets
- The only dataset that temperature scaling does not calibrate is the Reuters dataset
- Because this dataset is well-calibrated to begin with (ECE ≤ 1%)

<center>
<img
    src="image/Calibration/Fig4.png"
    width="50%"
/>

Figure 4. Reliability diagrams for CIFAR-100 before (far left) and after calibration (middle left, middle right, far right)
</center>

## Summary
 It remains future work to understand why these trends affect cali- bration while improving accuracy  
 Temperature scaling is the simplest, fastest, and most straightforward of the methods, and surprisingly is often the most effective  