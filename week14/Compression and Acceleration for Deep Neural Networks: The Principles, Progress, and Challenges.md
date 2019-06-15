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
The idea of using **transferred convolutional filters** to compress CNN models is motivated by recent works in [this paper](http://proceedings.mlr.press/v48/cohenc16.pdf). Following works inlcudes techniques like building a convolutional layer from a set of base filters.

Drawback: achieve competitive performance for wide/flat architectures (like VGGNet) but not narrow/special ones (like GoogleNet and ResNet); assumptions too strong.

<img src="https://i.imgur.com/xnVVvoJ.png" width=300>

## Knowledge distilation (KD)
KD is to compress deep and wide networks into shallower ones. [This work](https://arxiv.org/abs/1503.02531) introduced a KD compression framework, which eased the training of deep networks by following a student-teacher paradigm. Several works follows it but compression is done in terms of wide or depth.

Some also propose method to preserve knowledge in neurons instead of softened data. Some accelerate the training time or relax the assumption used in FitNet.

The Drawback: KD can only be applied to classification tasks with softmax loss function.

## Other types of approaches
- [Attention-based method] (http://proceedings.mlr.press/v48/almahairi16.pdf): learning to selectively focus or “attend to” a few, task-relevant input regions.
- Conditional computation: [N. Shazeer et al.](https://arxiv.org/abs/1701.06538) only computes the gradient for some important neurons. [dynamic DNNs (D2NNs)](https://ieeexplore.ieee.org/abstract/document/7423804/) were a type of feed-forward DNN that selected and executed a subset of D2NN neurons based on the input.
- Global average pooling  reduce the number of parameters of the fully connected layer.
- [Stochastic depth](https://link.springer.com/chapter/10.1007/978-3-319-46493-0_39) enabled the seemingly contradictory setup to train short networks and used deep networks at test time.
-  [FFT-based convolutions](https://arxiv.org/abs/1312.5851) and [Winograd algorithm](https://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Lavin_Fast_Algorithms_for_CVPR_2016_paper.html) reduce the convolutional overheads.

<img src="https://i.imgur.com/CeoJ9mn.png" width=300>
