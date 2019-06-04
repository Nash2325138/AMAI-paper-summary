# Efficient Convolutional Neural Networks for Mobile Vision Applications

## Introduction
This is the paper where Google propose the **MobileNets** architecture which focuses on improving model efficiency, including network size and runtime speed.
The proposed method also provide hyper-parameters to allow developers to choose the right size for their application.

---

## Prior work
Some privious approaches tried to **compress the network** or **train a smaller network** directly. Some used quantization of factorization to acheach smaller networks.

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

<img src="https://i.imgur.com/HWpdqyG.png" width=300 align=center>
