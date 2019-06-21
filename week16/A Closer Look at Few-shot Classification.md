# A Closer Look at Few-shot Classification
This work selects some existing few-shot learning works and design a cleaned experiment protocol to compare their performance.
A clear overview is given, along with some interesting discussion about the factors affecting the performance of few-shot
learning algorithms, such as the validation set **domain shfit**, network depth, and the distance-based modification to
the simple baseline.

---

### Intro
- Few-shot classification: Given abundant training examples for the base classes, few-shot learning algorithms aim to learn
to recognizing novel classes with a limited amount of labeled examples.
- Main challenges of fair comparison:
  - Underestimated baselines (e.g., training without data augmentation) and discrepancy of implementation details
  - The lack of domain shift between the base and novel classes -> unrealistic evaluation.
  
### Main contribution of this work:
- Provide a unified testbed for several different few-shot classification algorithms.
- It shows that a baseline method with little modification achieves competitive performance with the SOTAs.
- Construct validation set such taht the base and novel classes are sampled from different domains.

### Related work
Few-shot learning methods can be categorized into:
1. **Initialization based** methods `tackle the few-shot learning problem by “learning to fine-tune”`
2. **Distance metric learning based** methods makes their prediction by estimating the similarities between two entities.
3. **Hallucination based** methods learns a generator from data in the base classes to augment new novel class data.

This work is also related to **domain adaptation** since it tests and investigates the effect when domain shfit is present.

---

## Compared models

### Baseline and Baseline++
<img src="https://i.imgur.com/Pc66qVM.png" width=600>

The **baseline** model is simply composed of a image feature extractor (CNN) and a classifier (FC-layer with softmax).
The whole architecture is trained from scratch in the training stage by minimizing cross-entropy given base examples.
At fine-tuning stage, the featrue extractors are fixed and a new classifier is trained given labeled examples in novel classes.

The **baseline++** model is similar to the baseline model, but the classifier is replaced by computing the
*cosine similarity* between learned weights W and extracted features, which is claimed to **explicitly reduce intra-class variations**.

### Meta-learning methods 
<img src="https://i.imgur.com/ukuip8b.png" width=600>

There the authors take three distance metric learning based methods
([MatchingNet](https://arxiv.org/abs/1606.04080),
 [ProtoNet](https://arxiv.org/abs/1703.05175), and
 [RelationNet](https://arxiv.org/abs/1711.06025)) 
and one initialization based method ([MAML](https://arxiv.org/abs/1703.03400))

The spirit in the meta-learning is to sample small base support set and a base query set within randomly selected classes
in the training stage to **mimic the situation when predicting the novel classes**. In other words, `it makes the training procedure explicitly learn to learn from a given small support set.`

The difference between each meta-learning methods (MatchingNet, ProtoNet, and RelationNet) lies in their strategies to make prediction conditioned on support set as illustrated in the above picture.
And the initialization based method (MAML) use support set to adapt the model using few gradient updates.

---

## Experimental setup

### Datasets and scenarios.
- Use the mini-ImageNet for object recognition (100 classes from the ImageNet datasetand contains 600 images for each class)
- Use CUB-200-2011 for fine-grained classification (200 classes and 11,788 images in total)
- For cross-domain scenario,  use mini-ImageNet as our base class and the 50 validation and 50 novel class from CUB.

### Validate re-implementation
`Reproduced results to all few-shot methods do not fall behind by more than 2% to the reported results`

<img src="https://i.imgur.com/92rYvb2.png" width=800>

### Comparison
<img src="https://i.imgur.com/4zcq4Qm.png" width=800>

- Baseline++ improves the Baseline by a large margin, demonstrating that **reducing intra-class variation is an important factor** in the current few-shot classification problem setting.
- Baseline++ is competitive with other methods.

### Effect of Model Depth
<img src="https://i.imgur.com/9tT7mdJ.png" width=600>

- Intra-class variation decreases as backbone gets deeper (Davies-Bouldin index is a metric to evaluate the tightness
in a cluster)

<img src="https://i.imgur.com/Fieevow.png" width=800>

- In the CUB dataset, gaps among different methods diminish as the backbone gets deeper.
- In mini-ImageNet 5-shot, some meta-learning methods are even beaten by Baseline with a deeper backbone.

### Effect of Domain Shift
<img src="https://i.imgur.com/X2M2e9l.png" width=800>
- Meta-learning methods are not able to adapt to novel classes that are too different.
- Baseline quickly adapt to a novel class and is less affected by domain shift.

Conclusion: `as the domain difference
grows larger, the adaptation based on a few novel class instances becomes more important.`

### Further Adaption
-> Fix the features and train a new softmax classifier like Baseline does.

<img src="https://i.imgur.com/HeozFqA.png" width=500>

- Lack of adaptation is the reason meta-learning methods fall behind the Baseline in domain shift senario.
- The ProtoNet result shows that performance can degrade in scenarios with less domain difference. 

Conclusion: `learning to learn adaptation in the meta-training stage
would be an important direction for future meta-learning research in few-shot classification.`


