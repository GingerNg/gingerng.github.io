---
layout: post
title: "Multiple choice for entity match"
date:   2023-08-27
tags: [tech]
comments: true
author: GingerNg
---
In my [previous post about introduction of entity matching](https://blog.morethan.eu.org/entity_match/), tranditional entity matching process consists of data-processing, schema matching, blocking, record pair comparison and classification. Frequently, the process of pairwise comparison and classification is combined into a single **comparison** step in modeling.
Assuming, two data sources S and T will be merged.
The blocking process will reduce amount of computation by exclude impossible candidate entities. Assuming that, there will be N candidate entites for every entity of S. Even N is much smaller than |T|, for every entity from S, classification model will does N times inference for N candidate entities from T.

Inspired by **multiple choice** task in the field of MRC(Machine Reading Comprehension), we cast multiple binary classification tasks for the same entity into multiple choice task.

My [previous post](https://blog.morethan.eu.org/Is_ChatGPT_good_at_retrieve/) shows the potential of applying ChatGPT for ranking task which is similar as multiple choice task.

Therefore, A new method is proposed for entity matching after blocking. The multiple candidate entities for the same entity is merged into one sample, and we apply LLM for choosing the best option from them.

A rough prompt is designed inspired by [1], LLM is asked to choose the best entity.
```
You are EntityRankGPT, an intelligent assistant that can rank right products based on their relevancy to the left product.
Left is Mac book price 1999$
Rights are
[1] Mac book air, price 999$
[2] Mac studio, price 599$
[3] Mac mini, price 299$
Rank the 3 products above based on their relevance to the left product. The products should be listed in descending order using identifiers. The most relevant products should be listed first. The output format should be [] > [], e.g., [1] > [2]. Only response the ranking results, do not say any word or explain.
```

Noting: The above prompt is not the best.

##### references
[1] [RankGPT](https://github.com/sunnweiwei/RankGPT/blob/main/rank_gpt.py#L145)
