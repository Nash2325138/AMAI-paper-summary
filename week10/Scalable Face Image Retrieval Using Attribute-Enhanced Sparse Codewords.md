# Scalable Face Image Retrieval Using Attribute-Enhanced Sparse Codewords
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
as the human attribute) show that using human attributes can help the face retrieval task since the mutual information
(in another word, entropy of identity reduced after given gender attribute) is non-trivial.

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


