# [Paper reading] Learning to Hash for Indexing Big DataVA Survey

## Introduction
This is a survey paper about **learning to  hash**  framework  and  representative  techniques  of  various types, including **unsupervised, semi-supervised, and supervised**. 

----

## Background information
![Notation](./doc/T1_notations.png)

### Pipeline
1. Design hash functions
2. Generate hashcodes and indexing the database items
3. Online querying using hash codes

## Linear projection based
![](https://i.imgur.com/Hv0lriQ.png)

## Randomized Hashing
### Random Projection Based
![](https://i.imgur.com/eECAgH7.png)

### Random Permutation based Hashing


## Categories
A. Data-Dependent vs.  Data-Independen

B. Unsupervised, Supervised, and Semi-Supervised

C. Pointwise, Pairwise, Triplet-wise and Listwise
![](./doc/f4.png)

D. Linear vs. Nonlinear

E. Single-Shot Learning vs. Multiple-Shot Learning

F. Non-Weighted vs.  Weighted Hashing

## Prior methods
![](./doc/t2.png)
![](./doc/f6.png)

A.  Spectral Hashing

B.  Anchor Graph Hashing

C.  Angular Quantization Based Hashing
![](./doc/f7.png)

D.  Binary Reconstructive Embedding

E.  Metric Learning based Hashing
![](./doc/f8.png)

F.  Semi-Supervised Hashing
![](./doc/f9.png)

G.  Column Generation Hashing

H.  Ranking Supervised Hashin
![](./doc/f10.png)

I.  Circulant Binary Embedding

## Deep learning methods
![](./doc/t3.png)

## Advanced Methods
A.  Hyperplane Hashing
![](./doc/f13.png)

B.  Subspace Hashing

C.  MultiModality Hashing

## Applications
- image  search and retrieval
- patch matching, image classification, face recognition, pose estimation, object tracking, and duplicate detection
- cross-modality data fusion, large scale optimization, large scale classification and regression, collaborative filtering, and recommendation
