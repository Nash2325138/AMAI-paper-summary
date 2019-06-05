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


