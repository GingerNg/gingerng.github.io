---
layout: post
title: "chat my blog"
date:   2023-08-09
tags: [tech]
comments: true
author: GingerNg
---

This is a simple implementation of chat with my blog based on chromadb, cohere[1] and gradio.

#### Steps
- 1. collect & clean data, split texts into chunks
- 2. chunks embedding by cohere api, and save into chromadb
- 3. question embedding and recall chunks from chromadb
- 4. generate answer by feed question and recalled chunaks into cohere apis

#### example of cohere apis
Cohere embedding api can be easily intergated into chromadb:
```
cohere_ef = embedding_functions.CohereEmbeddingFunction(api_key=os.environ["COHERE_API_KEY"],
                                                        model_name="large")
client = chromadb.PersistentClient(path="***")
collection = client.get_or_create_collection(name="cohere_python", embedding_function=cohere_ef)
collection.count()
```
Add data into db:
```
collection.add(
    ids=["1", "2", "3"],
    documents=["Jack like apples",
               "Bob like bananas",
               "Mike like oranges"],
    metadatas=[{"fruit": "apple"},
               {"fruit": "banana"},
               {"fruit": "orange"}],
)
```
Recall document according to question:
```
print(collection.query(query_texts=["citrus"],
                       n_results=1))
```
Here is a designed prompt for answer question about documents by generate api.[2]
```
import cohere
co = cohere.Client(os.environ["COHERE_API_KEY"])
query = "where is ctrip?"
response = co.generate(
  prompt=f'Answer the question based only on the provided context, and not any other information.\n\
      The question is {query}. Here is all the context you have:\n\
        ctrip is a company located in nanjing.\n\
        The answer is:',
  max_tokens=100
)
print(response.generations.pop())
```
#### demo
Gradio is a useful tool to build simple UI for developers. We mock some data and test:
![cases-gradio](https://github.com/GingerNg/gingerng.github.io/blob/master/images/cohere_chroma_demo.png?raw=true)

##### references
- [1] [cohere](https://docs.cohere.com/reference/about)
- [2] [chat with your documents](https://github.com/chroma-core/chroma/tree/main/examples/chat_with_your_documents)