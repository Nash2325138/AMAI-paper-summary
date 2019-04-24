# [Paper reading] Learning to Hash for Indexing Big DataVA Survey

## Introduction
This is a survey paper about **learning to  hash**  framework  and  representative  techniques  of  various types, including **unsupervised, semi-supervised, and supervised**. 

----

## Background information
<img src="./doc/T1_notations.png" width=650>
### Pipeline
1. Design hash functions
2. Generate hashcodes and indexing the database items
3. Online querying using hash codes

## Linear projection based
![](https://i.imgur.com/Hv0lriQ.png)

## Randomized Hashing
### Random Projection Based
<img src="https://i.imgur.com/eECAgH7.png" width=400>

### Random Permutation based Hashing


## Categories
A. Data-Dependent vs.  Data-Independen

B. Unsupervised, Supervised, and Semi-Supervised

C. Pointwise, Pairwise, Triplet-wise and Listwise
<img src="/doc/f4.png" width=400>

D. Linear vs. Nonlinear

E. Single-Shot Learning vs. Multiple-Shot Learning

F. Non-Weighted vs.  Weighted Hashing

## Prior methods
<img src="/doc/t2.png" width=600>
<img src="/doc/f6.png" width=400>

A.  Spectral Hashing

B.  Anchor Graph Hashing

C.  Angular Quantization Based Hashing
<img src="/doc/f7.png" width=400>

D.  Binary Reconstructive Embedding

E.  Metric Learning based Hashing
<img src="/doc/f8.png" width=400>

F.  Semi-Supervised Hashing
<img src="/doc/f9.png" width=400>

G.  Column Generation Hashing

H.  Ranking Supervised Hashin
<img src="/doc/f10.png" width=400>

I.  Circulant Binary Embedding

## Deep learning methods
<img src="/doc/t3.png" width=400>

## Advanced Methods
A.  Hyperplane Hashing
<img src="/doc/f13.png" width=400>

B.  Subspace Hashing

C.  MultiModality Hashing

## Applications
- image  search and retrieval
- patch matching, image classification, face recognition, pose estimation, object tracking, and duplicate detection
- cross-modality data fusion, large scale optimization, large scale classification and regression, collaborative filtering, and recommendation
