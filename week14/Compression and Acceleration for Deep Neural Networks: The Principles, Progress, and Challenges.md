# Compression and Acceleration for Deep Neural Networks: The Principles, Progress, and Challenges

This is a survey paper which classified current neural networks compression or acceleration methods into 4 categories:
- Parameter pruning and sharing
- Low-rank factorization
- Transferred/compact convolutional filters
- Knowledge distillation
and gave the overviews for the four categories about how and where they are applicable.

---

## Parameter pruning and sharing
Mehtods under this category dedicate to exploring and reducing the redundenct given a network.

### Quantization and binarization
**Quantization** means to use a smaller bits for the representation of weights.
The idea comes from that actually the precision of floating points (32 bits) can be reduced to integer-precision (8 or 16 bits)
without a big loss of accruracy. Several experiments and appoaches like k-means scalar quantization and stochastic rounding-based
CNN training shows its effectivity.

The following figure shows the procudure adapted in [this paper](https://arxiv.org/abs/1510.00149) which has a convincing result.
<img src="https://i.imgur.com/aiAZmXf.png" width=700>

There are also several works investigating an extreme quantization senario: binary networks (quantized to 1-bit)
like  BinaryConnect, BinaryNet, and XNORNetworks. However, they usually get significantly lower performance compared
to the original network.

### Pruning and sharing
The idea in **pruning** and **weight sharing** is that there are ussually unused or non-informative weights hidden inside a large netwrok.
By pruning those weights of the networks, not only the complexity but also overfitting issues could be mitigated.
Adding **sparsity constraints** is also a popular option, e.g. otimizing the networks with L0 or L1 regularizers.

The drawback: some regularization requires more iterations to converge. Furthermore, all pruning criteria
require manual setup of sensitivity for layers, which is cumbersome.

### Designing the structural matrix
In fully-connected layers f(x, M) = sigma(Mx), the #parameters of M (= mn) and computational time (= O(mn)) is high. An m by n matrix that can be described using much fewer parameters than mn is called a *structured* matrix.
The drawback: loss in accuracy & no theoretical way to find a proper structural matrix.

## Low-rank factorization and sparsity
Idea: there might be a significant amount of redundancy in convolutional kernel tensor.
<img src="https://i.imgur.com/LkBQd3d.png" width=400>

The drawback: implementation is not easy because of a decomposition operation. Current methods perform low-rank only approximation layer by layer, not globally. Finally, it requires extensive model retraining to achieve convergence when compared to the original model.

## Transferred/compact convolutional filters
The idea of using **transferred convolutional filters** to compress CNN models is motivated by recent works in [this paper](http://proceedings.mlr.press/v48/cohenc16.pdf).
