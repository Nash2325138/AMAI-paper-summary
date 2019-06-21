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
can be categorized into:
1. **Initialization based** methods `tackle the few-shot learning problem by “learning to fine-tune”`
2. **Distance metric learning based** methods makes their prediction by estimating the similarities between two entities.
3. **Hallucination based** methods learns a generator from data in the base classes to augment new novel class data.

This work is also related to **domain adaptation** since it tests and investigates the effect when domain shfit is present.

---

##
