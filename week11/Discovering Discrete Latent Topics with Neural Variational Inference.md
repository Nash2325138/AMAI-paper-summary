# Discovering Discrete Latent Topics with Neural Variational Inference

Intro:
- Topic models: probabilistic generative models of documents.
- Traditional topic models use closed-form derivations for updating the models, but it's not scalable when the expressiveness grows
- This paper use NN to model **parameterisable** distributions over topics.
- This paper also propose to use RNN to discover **variable** number of topics.

---

## Parameterising Topic Distributions

Below are the formulation comparison between the traditional method LDA and the new proposed method.

In the aspect of **generative process**:

LDA: <img src="https://i.imgur.com/STt6YSB.png" width=300>

Proposed method: <img src="https://i.imgur.com/oqagOLr.png" width=300>

The difference: the **latent variables** theta_d is now sampled from G, which is composed of a **neural network**
conditioned on an isotropic Gaussian. (much like the decoder part of a VAE structure)

Tn the aspect of **marginal likelihood for a document in collection D**:

LDA: <img src="https://i.imgur.com/n2uoMwi.png" width=450>

Proposed method: <img src="https://i.imgur.com/ofDUxt3.png" width=450>
