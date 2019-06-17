# Scalable Face Image Retrieval Using Attribute-Enhanced Sparse Codewords
![](https://i.imgur.com/G7rGaBY.jpg)

This work detected **human attributes** automatically to improve content-based face retrieval
by constructing **semantic codewords** for efficient large-scale face retrieval.
The essential factors for face retrieval and effectiveness of different attributes are also experimented and discuseed.

Notion of **large-scale content-based face image retrieval**:
given a query face image, try to find similar face images from a large image database. 

Why? Low-level features used traditional methods are lack of semantic meaning.
This work incorporates high-level human attributes (illustrated below in (a)) into
face image representation and index structure. It compensate the information loss of preprocessed faces illustrated in (b)

<img src="https://i.imgur.com/8Q5r4gL.png" width=350>

But human attributes are non-trivial to apply because:
1. Human attributes only contain limited dimensions.
2. People might have similar attributes.
3. Human attributes are represented as a vector of floating points. It does not work well with developing large-scale indexing methods (results to slow response and scalability issue)

Therefore, this paper propose **attribute-enhanced sparse coding** and **attribute-embedded inverted indexing** to solve these issues.

## Observations
Prior works crop only the facial region and normalize the face into the same position
and illumination. which ignores the rich semantic cues decribed in figure above.

Also, the following statics (entropy and mutual information computed from two datasets s using only gender
as the human attribute) show that using **human attributes can help the face retrieval task since the mutual information**
(in another word, entropy of identity reduced after given gender attribute) **is non-trivial**.

<img src="https://i.imgur.com/4ofApi9.png" width=350>

## Proposed method

### System architecuture
<img src="https://i.imgur.com/1udgZfb.png" width=800>
The caption in the figure nicely describes the overall system architecture and the processing flow:

```
Both query and database images will go through the same procedures including face detection,
facial landmark detection, face alignment, attribute detection, and LBP feature extraction.

Attribute-enhanced sparse coding is used to find sparse codewords of database images globally in the offline stage.
Codewords of the query image are combined locally with binary attribute signature to traverse the attribute-embedded
inverted index in the online stage and derive real-time ranking results over database images.
```

### Attribute-Enhanced Sparse Coding (ASC)
ASC is realized by optimizing the following objective:

<img src="https://i.imgur.com/Qgupe76.png" width=450>

Notion: dictionary D and sparse feature encoding V. Then, a feature is a linear combination of
the column vectors of the dictionary.

A few of details:  different spatial grids := 175, #centrois K := 1600.
Therefore, the vocabulary size will be 175 * 1600 = 280000

### Attribute-Enhanced Sparse Coding
First proposal: dictionary selection (ASC-D) force images with different attribute values to contain different codewords by using different subsets for postive and negative samples separately (as illustrated below):
<img src="https://i.imgur.com/7adOMQh.png" width=250>

(For attributes with multiple values, it simply devides multple subsets for different values.)

This goal can be formulated as:

<img src="https://i.imgur.com/r1GFfxe.png" width=450>

Drawback:
- not robust to possible attribute detection errors.
- encodes only binary indicators but relative confidence scores are needed.

Therefore, the author propose a soft weighted version (ASC-W), where the distance between attribute scores of the image
and the attribute scores assigned to the dictionary centroids are used as the weights for selecting codewords: <img src="https://i.imgur.com/eorIVo0.png" width=200>

The fomulation:

<img src="https://i.imgur.com/dvfWRsu.png" width=450>

### Attribute Embedded Inverted Indexing (AEI)
1. Image Ranking and Inverted Indexing: use a codeword set to represent computed the sparse representation of an image.
The similarity between two images:  <img src="https://i.imgur.com/4ZAZYpV.png" width=200>
2. Attribute-Embedded Inverted Indexing:
use a binary signature to represent its human attribute b: <img src="https://i.imgur.com/LX0rVxQ.png" width=200>,
and the similarity score becomes: <img src="https://i.imgur.com/Co5Rj1c.png" width=350>

## Experiments
Compare to baselines:

<img src="https://i.imgur.com/Ec19b57.png" width=500>

Performance of single attribute:

<img src="https://i.imgur.com/unKapPM.png" width=600>

Using multiple attributes:

<img src="https://i.imgur.com/NOqeeLJ.png" width=400>

Attribute-Embedded Inverted Indexing:

<img src="https://i.imgur.com/DCdBA6C.png" width=400>

The paper also showcases its scalibility in terms of memory usage, and online retrieval time in the last few subsections.
