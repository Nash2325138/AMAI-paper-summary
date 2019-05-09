# [Paper reading] Graph Embedding and Extensions: A General Framework for Dimensionality Reduction

## Introduction
This is a survey paper about **dimensionality reduction** methods (e.g. PCA, LDA, LPP, ISOMAP, LLE) framework under an general **graph embedding** formulation. It also presented a new supervised approach called **Marginal Fisher Analysis**.

----

## Unified graph embedding formulation
![](https://i.imgur.com/tBp7cgu.png)

### Definitions
F: x -> y, x \in R^n, y \in R^m, where m << n
![](https://i.imgur.com/wZkOthD.png)

### Optimization goal
![](https://i.imgur.com/UCYFm6d.png)
where, d is constant, B is constant matrix

### Linearization: F: x -> y = W^T * x
The optimization becomes
![](https://i.imgur.com/ymBs5wD.png)

Efficient, but performance not easy to scale.

### Kernelization
kernel k(xi, xj) = phi(xi) * phi(xj)
mapping direction w = sum_i(alpha_i * phi(xi))
-> kernel Gram Matrix K_i,j = phi(xi) * phi(xj)
The optimization becomes
![](https://i.imgur.com/2DveVR8.png)

### Optimization solution
![](https://i.imgur.com/QuJHITu.png)

### Tensorization
Vertix representation could also be matrix (second-order tensor) like image or even third-order tensor like video.

#### Some tensor terminology
In this subsection provide lots of termiology for tensor operations, including
- Inner product
- Norm or Frobenius norm in second-order tensor
- Distance

Using there definitions, the above formulation can be refomulated.

## Prior methods
The following **dimension reduction** works can actually reformulated by the graph embedding framework

- PCA
- LDA
- ISODMAP
- LLE and LEA
- Laplacian Eigenmap

## Motivations of studying hashing

## High-level overview of learning-based hashing methods

## Learning to hash framework

## Deep learning methods

## Open issues
