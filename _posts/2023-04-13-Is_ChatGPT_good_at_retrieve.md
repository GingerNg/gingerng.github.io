---
layout: post
title: "Is ChatGPT good at retrieve"
date:   2023-04-24
tags: [Tech]
comments: true
author: GingerNg
---

Recently, 2 new papers discussing applying chatgpt for retrieve have been released, this post will summary them.

#### Is ChatGPT Good at Search? Investigating Large Language Models as Re-Ranking Agent
The experiment of this paper reveal that properly instructed ChatGPT and GPT-4 can deliver competitive, even superior results than supervised methods on popular IR benchmarks.
![](https://s2.loli.net/2023/04/23/ovg8pOWtHdlDcb2.png)
Also, as the limit of input length of ChatGPT api, this paper propose a sliding window strategy(as shown below) which can be consider an approximation of ranking all passages.

![](https://s2.loli.net/2023/04/23/5qt8vzgI6c7U1WE.png)

#### Is ChatGPT a Good Recommender? A Preliminary Study
There exists five types of recommendation tasks: rating prediction, direct recommendation, sequential recommendation, review summary and explanation generation.
Compared to direct Recommendation, sequential recommendation takes into account the order of item consumption or interaction to generate more personalized and relevant recommendations.
In this paper, the experimental results show that ChatGPT performs well in rating prediction but poorly in sequential and direct recommendation tasks, indicating the need for further exploration and improvement.

#### Thought
The conclusion of the two papers is slightly different, ChatGPT can achieve SOTA (State-of-the-Art) performance in search/retrieval tasks, but needs further exploration and improvement for sequential and direct recommendation tasks. However, search and recommendation are quite similar tasks and both can be abstracted as the ranking or matching problem. There is still much room for improvement in the field of natural language processing. NLP is still alive.

