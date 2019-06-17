# Device-Aware Progressive Search for Pareto-Optimal Neural Architectures
This paper augues that most for current SOTA of NAS algorithm do not consider much on
**device-related objectives** such as inference time, memory usage, and power consumption.
A new architecture, DPPNet: Device-aware Progressive Search for Pareto-optimal Neural Architectures,
is proposed to optimize on device-related objectives by using more compact search space and adopting progressive search.

Concepts introduction:
- Approaches for NAS are mainly based on Reinforcement Learning (RL) or Genetic Algorithm (GA).
- Pareto-frontier of error rate v.s inference time could vary between different devices (as illustrated below)

<img src="https://i.imgur.com/kAfbred.png" width=400>

The authors declairs that DPPNet is an efficient search algorithm architectures at the Pareto-front 
to explore the trade-off among these objectives, which is pratical for deep learning practitioners.

---

## Search Architecture
The connecting rules follow the design of CondenseNet, and 2 base archtectures are used for CIFAR10 and ImageNet
<img src="https://i.imgur.com/aIHT3DC.png" width=600>

## Search Space
The search space is designed to conver the two well-known efficient convolution operations,
i.e. Depth-wise Convolution and Learned Group Convolution.

Search space of one normalization layer:
1. Batch Normalization + Relu
2. Batch Normalization
3. No op (Identity)

Search space of one convolutional layer:
1. 1x1 Convolution
2. 3x3 Convolution
3. 1x1 Group Convolution
4. 3x3 Group Convolution
5. 1x1 Learned Group Convolution
6. 3x3 Depth-wise Convolution

#### Comparison to other well-known CNN blocks
<img src="https://i.imgur.com/svMq2ZL.png" width=500>

## Search algorithm
<img src="https://i.imgur.com/kDTTQje.png" width=700>

The search algorithm applied Sequential Model-Based Optimization and is composed of 3 steps:
1. Train and Mutation: K models with #layers=l will be trained. To mutate, one layer
(conv or norm, depending on the last layer) will be added and therefore there will
be 3 (norm is added) or 6 (conv is added) times of number of models after mutation.
2. Update and Inference: To evaluate the mutated models, a **surrogate function** is used to 
avoid time-consuming training to obtain true accuracy of a network.
3. Model Selection:
