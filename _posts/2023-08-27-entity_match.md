---
layout: post
title: "Introduction of entity match"
date:   2023-08-27
tags: [tech]
comments: true
author: GingerNg
---
Entity matching, also known as record linkage, is a crucial aspect of Natural Language Processing (NLP) that involves identifying and connecting data to determine whether two entities refer to the same real-world object or not.[1]
![example-1](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*7TzI0bUFkmAKAg3M.jpg)

#### Problem definition
Let $𝐴$ and $𝐵$ be two data sources.
𝐴 has the attributes $(𝐴_1, 𝐴_2, ..., 𝐴_𝑛)$, and we denote records as $𝑎 = (𝑎_1, 𝑎_2, ..., 𝑎_𝑛) ∈ 𝐴$.
Similarly, $𝐵$ has the attributes $(𝐵_1, 𝐵_2, ..., 𝐵_𝑚)$, and we denote records as $𝑏 = (𝑏_1, 𝑏_2, ..., 𝑏_𝑚) ∈ 𝐵$.
$A$ data source is a set of records, and a record is a tuple following a specific schema of attributes. An attribute is defined by the intended semantics of its values. So $𝐴_𝑖 = 𝐵_𝑗$ if and only if values $𝑎_𝑖$ of $𝐴_𝑖$ are intended to carry the same information as values $𝑏_𝑗$ of $𝐵_𝑗$, and the specific syntactics of the attribute values are irrelevant. Attributes can also have metadata (like a name) associated with them, but this does not affect the equality between them. We call the tuple of attributes $(𝐴_1, 𝐴_2, ..., 𝐴_𝑛)$ the schema of data source $𝐴$, and correspondingly for $𝐵$. The goal of entity matching is to find the **largest possible binary relation** $𝑀 ⊆ 𝐴 × 𝐵$ such that $𝑎$ and $𝑏$ refer to the same entity for all $(𝑎, 𝑏) ∈ 𝑀$.[2]
Obviously, the number of candidate all potential pairs is Cartesian product $|𝐴 × 𝐵|$.

#### Traditional entity matching process
Tranditional entity matching process consists of data-processing, schema matching, blocking, record pair comparison and classification.
- **Schema matching** is aimed to  find out which attributes should be compared to one another, essentially identifying semantically related attributes. In practice, this step is often performed manually as part of the preprocessing step, simply making sure to transform both data sources into the same schema format.

- Since the number of potential matches grows quadratically, it is common to pick out candidate pairs $𝐶 ⊆ 𝐴 × 𝐵$ in a separate step before any records are compared directly. This step is called as **blocking**, and its goal is to bring down the number of potential matches $|𝐶| ≪ |𝐴 × 𝐵|$ to a level where record-to-record comparison is feasible.
- When the number of candidate pairs $|𝐶|$ has been reduced to a manageable amount, we can compare individual records $(𝑎, 𝑏) ∈ 𝐶$. The **pairwise comparison** results in a similarity vector $𝑆$, consisting of one or more numerical values indicating how similar or dissimilar the two records are.
- Lastly, the objective of the **classification** step is to classify each candidate pair as either match or nonmatch based on the similarity vector. In cases where |𝑆 | = 1, simple thresholding might be enough, while when |𝑆 | > 1, one needs more elaborate solutions.
Frequently, the process of pairwise comparison and classification is combined into a single **comparison** step in modeling.
In the overall process, the two key components are **blocking** and **comparison**.

![trandition_entity_match_pipeline](https://github.com/GingerNg/gingerng.github.io/blob/master/images/trandition_entity_match_pipeline.png?raw=true)

#### Metrics
For blocking:
- $PR = |C|/|𝐴 × 𝐵|$
- $P/E = |C|/|𝐴|$

For comparsion:
- precision/recall measures
- $F_1$



#### Datasets
The early approaches to entity matching were mostly concerned with matching personal records(census data or medical records). Such datasets are usually not publicly available due to privacy concerns.[2]
An overview of the most popular public datasets has been listed below:
![ public datasets](https://github.com/GingerNg/gingerng.github.io/blob/master/images/public%20entity%20match%20dataset.png?raw=true)






- [1] [Entity Matching : From Traditional Techniques to Deep Learning Solutions](https://www.invivoo.com/en/entity-matching-traditional-techniques-deep-learning-solutions/)
- [2] [Neural Networks for Entity Matching: A Survey](https://arxiv.org/abs/2010.11075)
- [3] [Entity Matching](https://medium.com/@mansijain.1213/entity-matching-fa89cae188eb)