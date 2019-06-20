# Bidirectional Attention Flow for Machine Comprehension
This works proposed a new architecture **Bi-Directional Attention Flow (BIDAF) network** to solve the 
problem **machine comprehension (MC)** (e.g. SQuAD dataset). The performance (compared to current methods in 2019) is not the best,
but the significance lies on the proposal of **bi-directional attention** and its insight when dealing with language
tasks, which has an great impact on future models.

---

Intro:
- Machine comprehension (MC): given a query and a context (both are orderd sets of words), the goal is to answer the query based on the context.
- SQuAD dataset: in SQuAD, answers come from a part of original contexts.

---

## Architecture
BIDAF is a hierarchical multi-stage architecture composed of 6 layers to model the **query-aware context** representations
of the context paragraph at **different levels of granularity**:

<img src="https://i.imgur.com/wwXi9nm.png" width=800>

1. Character Embedding Layer
2. Word Embedding Layer
3. Contextual Embedding Layer
4. Attention Flow Layer
5. Modeling Layer
6. Output Layer

#### Character Embedding Layer and Word Embedding Layer
The two embedding layers aim to obtain the low-level representation of input paragraphs for both the context and the query.
Character embedding layer takes 1d CNN as its extrator. Word embedding layer applies GloVe to get the output.
Both of therir outputs are fix-length vectors.

#### Contextual Embedding Layer
Both of outputs from previous embedding layers are them fed to the contextual embedding layer, which is
essentially bi-directional LSTM.

Combined with the first two layers, the output could be seen as features containning different levels of granularity.

### Attention Flow Layer
Attention flow layer is the main novelty in this paper and it's responsible for linking and fusing information
from the context and the query words.
Instead of directly summarizing the query and context into single feature vectors like previous attention machenisms do,
the proposed attention vector `are allowed to flow through to the subsequent modeling layer. This reduces the information loss caused by early summarization.`

In details, this layer first compute a **similarity matrix S** between the contextual embeddings of the **context (H)** and the **query (U)** by
<img src="https://i.imgur.com/wuzLTYA.png" width=150>
, where S_t,j indicates the similarity between t-th context word and j-th query word.
, and the function alpha is defined as 
<img src="https://i.imgur.com/D5LuuIN.png" width=200>.

The similarity matrix S is then used to compute the following **Context-to-query (C2Q) attention** and **Query-to-context (Q2C) attention**

Context-to-query (C2Q) attention:
Query-to-context (Q2C) attention:
