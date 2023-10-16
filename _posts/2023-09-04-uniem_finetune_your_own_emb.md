---
layout: post
title: "Uniem: finetune your own embedding model"
date:   2023-09-04
tags: [tech]
comments: true
author: GingerNg
---

In my [previous blog](https://blog.morethan.eu.org/text_semantic_similarity/), we introduced the semantic similarity of text about cosine distance. However, it's only about how to measure the similarity of vectors. The step of how to get the embedding of text is more important.

Transformer has been the mainstream NN structure in DL field, and also has produced  many good pretrained embedding models such as M3E[4], text2vec-large-chinese[5] and so on. We can use these pretrained models directly for common tasks but domain tasks. It's necessary to finetune modele on domain datasets.

Recently, we find an easy-use package named uniem[1] to finetune your own embedding model just like code below.
```
from datasets import load_dataset

from uniem.finetuner import FineTuner

dataset = load_dataset('shibing624/nli_zh', 'STS-B')
# 指定训练的模型为 m3e-small
finetuner = FineTuner.from_pretrained('moka-ai/m3e-small', dataset=dataset)
finetuner.run(epochs=3)
```

##### supported data format
- PairRecord: sentence pair
- TripletRecord: sentence triple with one positive and one negative
- ScoredPairRecord，sentence pair with score

##### train from scratch
If you want train your model from scratch, use the code below:
```
from datasets import load_dataset
from transformers import AutoTokenizer

from uniem.finetuner import FineTuner
from uniem.model import create_uniem_embedder

dataset = load_dataset('shibing624/nli-zh-all', streaming=True)
dataset = dataset.rename_columns({'text1': 'sentence1', 'text2': 'sentence2'})

# 由于是从头训练，我们需要自己初始化 embedder 和 tokenizer。当然，我们也可以选择新的 pooling 策略。
embedder = create_uniem_embedder('uer/chinese_roberta_L-2_H-128', pooling_strategy='cls')
tokenizer = AutoTokenizer.from_pretrained('uer/chinese_roberta_L-2_H-128')

finetuner = FineTuner(embedder, tokenizer=tokenizer, dataset=dataset)
fintuned_model = finetuner.run(epochs=3, batch_size=32, lr=1e-3)
```

Uniem is an package based on sentence-transformers[2] and accelerate[3]. 'EmbedderForTrain' is its core class which holds embedder and criterion.
```
class EmbedderForTrain(torch.nn.Module):
    embedder: Embedder

    def __init__(
        self,
        embedder: Embedder,
        criterion: torch.nn.Module,
    ):
        super().__init__()
        self.embedder = embedder
        self.criterion = criterion
```

##### references
- [1][uniem](https://github.com/wangyuxinwhy/uniem)
- [2][sentence-transformers](https://www.sbert.net/)
- [3][accelerate](https://github.com/huggingface/accelerate)
- [4][m3e-base](https://huggingface.co/moka-ai/m3e-base)
- [5][text2vec-large-chinese](https://huggingface.co/GanymedeNil/text2vec-large-chinese)
