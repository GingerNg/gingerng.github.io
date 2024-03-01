---
layout: post
title: " LLM cocktail"
date:   2024-03-01
tags: [tech, paper reading]
comments: true
author: GingerNg
---

Recently, I found an interesting paper[2] from twitter[1]. Below are my notes.

### Catastrophic Forgetting
The “pre-training and fine-tuning” paradigm is applied in may applications. However, the fine-tuning operation could lead to severe degeneration of LM’s general capabilities beyond the targeted domain. Such a phenomenon is commonly referred as catastrophic forgetting. It is also called "alignment tax" in the paper of InstructGPT[3].
This paper proposes a model merging method named **LLM-Cocktail**[2] which can mitigate the problem of catastrophic forgetting.
### Cocktail Paradigm
![vanilla form](https://img.morethan.eu.org/file/tech-imgs/vanilla+form.png)
![code](https://pbs.twimg.com/media/GAMPeWeXUAAqhwV?format=jpg&name=large)

### Performace
The resilient-tuned model via LLM-Cocktail outperforms both base model and fine-tuned model in 8 different fine-tuning target tasks. Meanwhile LLM-Cocktail(only merging the base model and fine-tuned model) achieves best in 7(not fine-tuning) other tasks.
![performace](https://img.morethan.eu.org/file/tech-imgs/cocktail-performace.png)

### Comment
From the view of ensembling, LLM-Cocktail is a weight-space model ensembling method. Conventional ensembling method usually combine the outputs of many models to improve the performance. The drawback is the cost of inference increases rapidly. Weight-space model ensembling method can avoid this drawback.


##### references
- [1][twitter](https://twitter.com/9hills/status/1730243893126430831)
- [2][LM-Cocktail: Resilient Tuning of Language Models via Model Merging](https://arxiv.org/abs/2311.13534)
- [3][InstructGPT Training language models to follow instructions with human feedback](https://arxiv.org/abs/2203.02155)