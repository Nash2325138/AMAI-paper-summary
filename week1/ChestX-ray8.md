# [Paper reading] ChestX-ray8
ChestX-ray8: Hospital-scale Chest X-ray Database and Benchmarks on Weakly-Supervised Classification and Localization of Common Thorax Diseases

Xiaosong Wang, Yifan Peng, Le Lu, Zhiyong Lu, Mohammadhadi Bagheri, and Ronald M. Summers, CVPR 2017

## Contribution
In the domain of medical images, labeled datas are usually valuable because of the needs of professional annotations. This paper use some NLP technique to text-mine data from associated radiological reports and presents a **new chest database named "ChestX-ray8"** comprising a large amount of labeled data (around 109k images with 33k unique patients).
Besides the provided dataset, the authors also presents **unified framework** to solve a weakly-supervised multi-label image classification and pathology localization problem.

## Method
### Database constuction

#### Results
<p align="center">
  <img src="https://i.imgur.com/TWSeUum.png" width="400">
</p>

### Unified framework
![](https://i.imgur.com/eo6bR7e.png)

#### Transition layer
A set of convolutional layers to make to transform the activation of different pre-trained CNN architecture to the same shape

#### Pooling layer: spatially global pooling
- Log-Sum-Exp(LSE) pooling
<p align="center">
  <img src="https://i.imgur.com/BfTY9Lp.png" width="400">
</p>

- Improved LSE pooling (to prevent underflow/overflow problem) is used instead of regular LSE
<p align="center">
  <img src="https://i.imgur.com/mYGzuir.png" width="400">
</p>

#### Prediction layer
A fully connected layer from globally pooled features to 8 disease scores.

#### Multi-label Classification Loss
While regular cross entropy loss (CEL) can be applied, the paper uses weighted CEL (W-CEL) to deal with the negative-dominated dataset.
<p align="center">
  <img src="https://i.imgur.com/oJbbaqv.png" width="400">
</p>

#### Results
![](https://i.imgur.com/7vbNhOE.png)
