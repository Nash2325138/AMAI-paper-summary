# Efficient Convolutional Neural Networks for Mobile Vision Applications

## Introduction
This is the paper where Google propose the **MobileNets** architecture which focuses on improving model efficiency, including network size and runtime speed.
The proposed method also provide hyper-parameters to allow developers to choose the right size for their application.

---

## Prior work
Some privious approaches tried to **compress the network** or **train a smaller network** directly. Some used quantization of factorization to acheach smaller networks.

## MobileNet Architecture
The core layer of MobileNet is **Depthwise Separable Convolution**

### Depthwise Separable Convolution
Depthwise Separable Convolution means a convolution factorized into **depthwise** and **pointwise** convolution as illustrated below.

<img src="https://i.imgur.com/ISzRO4E.png" width=400>
