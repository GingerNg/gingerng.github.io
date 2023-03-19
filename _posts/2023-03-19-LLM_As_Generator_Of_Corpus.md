---
layout: post
title: "Apply LLM as Generator of Corpus"
date:   2023-03-19
tags: [geek]
comments: true
author: GingerNg
---

LLMs have been applied in many fields such as chatbot, information extraction[1] and so on.

Here, this post list some works which directly apply LLMs as generator of corpus.


##### ChatAug
**ChatAug**[2] apply [ChatGPT](https://openai.com/blog/chatgpt) for data augmentation. As the framework show below, this work input samples into [ChatGPT](https://openai.com/blog/chatgpt) and prompt [ChatGPT](https://openai.com/blog/chatgpt) to generate samples that preserves semantic consistency with inputed sample.
![](https://s2.loli.net/2023/03/19/ZOqzWnyxlG5uIQj.png)


##### Self-Instruct
**Self-Instruct**[3] is a semi-automated process for instruction-tuning a pretrained LM using instructional signals from the model itself.
![](https://s2.loli.net/2023/03/19/FKyLP1UvWeTn4MA.png)
 Its process starts with a small seed set of tasks (one instruction and one input-output instance for each task) as the task pool. Random tasks are sampled from the task pool, and used to prompt an off-the-shelf LM to generate both new instructions and corresponding instances, followed by filtering low-quality or similar generations, and then added back to the initial repository of tasks. The resulting data can be used for the instruction tuning of the language model itself later to follow instructions better.
 **Alpaca**[4] model is trained on 52K instruction-following demonstrations generated in the style of self-instruct using text-davinci-003.
 ![](https://s2.loli.net/2023/03/19/AE7jJY3TpdNH8VD.png)

Although [ChatGPT](https://openai.com/blog/chatgpt) can be applied for almost every nlp task, many researchers have found that [ChatGPT](https://openai.com/blog/chatgpt) can't beat the SOTA model of specific task like translation. However, LLMs can push the improvement of specific tasks.

##### references
[1] Zero-Shot Information Extraction via Chatting with ChatGPT
[2] ChatAug: Leveraging ChatGPT for Text Data Augmentation--2023
[3] SELF-INSTRUCT: Aligning Language Model with Self Generated Instructions--2022
[4] [Alpaca: A Strong, Replicable Instruction-Following Model](https://crfm.stanford.edu/2023/03/13/alpaca.html)