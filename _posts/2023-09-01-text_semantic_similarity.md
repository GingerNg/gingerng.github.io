---
layout: post
title: "Text semantic similarity"
date:   2023-09-04
tags: [tech]
comments: true
author: GingerNg
---
#### Semantic Similarity
Cosine similarity is commonly used for semantic similarity because it offers several advantages in measuring the similarity between vectors, particularly in natural language processing (NLP) and information retrieval tasks. Here are some reasons why cosine similarity is widely used for semantic similarity:

1. Independence of vector length: Cosine similarity is insensitive to the magnitude or length of vectors. It only considers the angle between vectors, making it suitable for comparing vectors regardless of their scale. This property is beneficial when dealing with high-dimensional vector representations, such as word embeddings or document vectors.

2. Angle-based measure: Cosine similarity measures the cosine of the angle between two vectors, which can be interpreted as a measure of similarity in the direction of the vectors. When vectors point in similar directions, the cosine similarity is closer to 1, indicating high similarity. Conversely, when vectors are orthogonal (angle of 90 degrees), the cosine similarity is 0, indicating no similarity.

3. Efficient computation: Computing cosine similarity is computationally efficient, especially for sparse vectors or large-scale datasets. It involves simple vector operations, such as dot products and norms, which can be efficiently computed using linear algebra libraries.

4. Robustness to dimensionality: Cosine similarity is known to be more robust to the curse of dimensionality compared to other distance metrics. As the dimensionality of the vectors increases, the Euclidean distance becomes less meaningful, while cosine similarity remains effective in capturing the semantic relationships among vectors.

5. Applicability to text data: Cosine similarity is well-suited for text data analysis because it can capture semantic similarity based on the distributional hypothesis. By representing words or documents as high-dimensional vectors (e.g., word embeddings), cosine similarity can effectively measure their semantic relatedness based on their distributional patterns in a corpus.

Overall, cosine similarity provides a simple and effective measure for capturing semantic similarity between vectors, making it a popular choice in various NLP tasks, such as document similarity, information retrieval, clustering, and recommendation systems.[2]

##### Cosine similarity
Cosine similarity, measures the similarity between two vectors by calculating **the cosine of the angle between them**. There are two different types for different scenario.

##### dot cosine
Cosine similarity is computed using the dot product of the vectors divided by the product of their magnitudes. The formula for dot cosine similarity is:
cosine_similarity = dot_product(A, B) / (magnitude(A) * magnitude(B))
Magnitude is the L2 norm can be caculated as ||V||₂ = sqrt(sum(V[i]^2)) for i = 1 to n.
The comment of dot cosine is:
Computes the cosine similarity cos_sim(a[i], b[j]) for all i and j.
:return: Matrix with res[i][j]  = cos_sim(a[i], b[j])

If we have the following vectors:
```
embedding_1 = np.array([[3, 1, 2], [3, 1, 2]])
embedding_2 = np.array([[ 4, 6, 1]])
```
```
from sentence_transformers import util
util.pytorch_cos_sim(embedding_1, embedding_2)
```
The implemention of dot cosine based on numpy is below:
```
from numpy import dot,sqrt,mat
from numpy.linalg import linalg
dot(embedding_1, embedding_2.T) / (linalg.norm(embedding_1) * linalg.norm(embedding_2))
```
##### pair-wise cosine
Pair-wise cosine is quite similar as above, but the caculation bewteen vectors pair by pair. The A and B should have the same size. The inputs with same index will be compared.
The comment of pairwise cosine is:
Computes the pairwise cossim cos_sim(a[i], b[i])
:return: Vector with res[i] = cos_sim(a[i], b[i])
```
from sentence_transformers import util
util.pairwise_cos_sim(embedding_1, embedding_2)
```
```
np.sum(np.multiply(embedding_1, embedding_2), axis=-1) / (np.linalg.norm(embedding_1, axis=1) * np.linalg.norm(embedding_2, axis=1))
```

**NOTE**: although the function cosine_similarity of sklearn belongs to pairwise submodule, it is not pair-wise cosine.
```
from sklearn.metrics.pairwise import cosine_similarity
cosine_similarity(embedding_1, embedding_2)
```

- [1][sentence_transformers-utils](https://huggingface.co/tasks/sentence-similarity)
- [2][Why cosine is the most used semantic similarity](https://poe.com/s/E2HKIvYrjNf9eGsDhrqG)