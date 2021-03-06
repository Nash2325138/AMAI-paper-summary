# Efficient Convolutional Neural Networks for Mobile Vision Applications

## Introduction
This is the paper where Google proposes the **MobileNets** architecture which focuses on improving model efficiency, including network size and runtime speed.
The proposed method also provides hyper-parameters to allow developers to choose the right size for their application.

---

## Prior work
Some previous approaches tried to **compress the network** or **train a smaller network** directly. Some used quantization or factorization to achieve smaller networks.

## Depthwise Separable Convolution
The core layer of MobileNet is **Depthwise Separable Convolution**, which is a convolution factorized into **depthwisely** and **pointwisely** as illustrated below.

<img src="https://i.imgur.com/IIPT6gc.png" width=400 align=center>

(pointwise convolution is essentially 1 by 1 convolution)

Let input feature size be D_F x D_F x M, the kernel size be D_K x D_K x N
The computation cost of original convolution will be <img src="https://i.imgur.com/zkCstde.png" width=180>

While **depthwise** convolution have <img src="https://i.imgur.com/G2ctsmG.png" width=150>.

Including **pointwise** convolution, the cost becomes  <img src="https://i.imgur.com/8moBLQk.png" width=250>

The overall cost reduction ratio becomes <img src="https://i.imgur.com/0gHu2JK.png" width=250>

## MobileNet Architecture
The MobileNet architecture is composed of Depthwise Separable convolutions with Depthwiseand Pointwise layers followed by batchnorm and ReLU like <img src="https://i.imgur.com/I0nnA2K.png" width=100>.

The overall architecture is described in this table:

<img src="https://i.imgur.com/HWpdqyG.png" width=300>

## Hyper-parameters
The parameters that determine the size of MobileNet include **width multiplier** alpha and **resolution multiplier** ro, which reduce the **channel number** and **feature width/height** uniformly on each convolution layer to achieve smaller and faster model.

## Experiments
The authors provide plenty of experiments to justify their contribution, including abundant ablation studies:

<img src="https://i.imgur.com/HjZ5ng3.png" width=350>

### Trade off between accuracy and model size / operation count
<img src="https://i.imgur.com/iYORY9v.png" width=250> <img src="https://i.imgur.com/t3hqIMD.png" width=250>

### Comparison with popular (performance oriented / compression oriented)
<img src="https://i.imgur.com/RCfzcEj.png" width=350>

#### With different hyper-parameters
<img src="https://i.imgur.com/RqD95xn.png" width=350>

### Comparison with other SOTAs on other tasks
- PlaNet
<img src="https://i.imgur.com/r4apvLn.png" width=300>

- Stanford Dogs (fine grained)
<img src="https://i.imgur.com/PBSWFFX.png" width=300>

- COCO object detection
<img src="https://i.imgur.com/bDXTdQl.png" width=300>


## Conclusion
The paper proposed a computationally and spatially efficient model that is flexibly configurable. Quite enough experiments are provided, and the result is convincing.
