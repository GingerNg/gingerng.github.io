---
layout: post
title: "Open Source ChatGPT Code Interpreter Plugin"
date:   2023-08-30
tags: [tech]
comments: true
author: GingerNg
---
As LLM(Large Language Model) has great performance of generation, code generation product like **github copilot** has become a powerful tool for programmer which can help them save much time.

Usually, programers get the generated code and run or test them manually. Can LLM generate code and execute automatically?

OpenAI demonstrated us the **code-interpreter** which provide their models with a working Python interpreter in a sandboxed, firewalled execution environment, along with some ephemeral disk space.[1]
As the below shown, LLM generate solution code of the question and code-interpreter executes them automatically and return answer the asker.
![code-interpreter-1](https://github.com/GingerNg/gingerng.github.io/blob/master/images/chatgpt-code-interpreter-1.png?raw=true)
![code-interpreter-2](https://github.com/GingerNg/gingerng.github.io/blob/master/images/chatgpt-code-interpreter-2.png?raw=true)
#### Compaired with function call
Function call[5] is a new feature of openai-api, which help us parse parameters and choose function according natural language query/question. We have to provide openai-apis the description of our functions and implement them before. Function can be anything: fetching data, caculation, code execution, and so on. Programmers still have to write the code of calling. Obviously, code-interpreter is a further step. With code-interpreter, function will be generated in the form of code. Even, code-interpreter only support python now, it will not stop here.

We found several open source implementation of code-interpreter.

#### gpt-code-ui
gpt-code-ui is a open source implementation of OpenAI's ChatGPT Code interpreter.[2]

#### plotai
Plotai is a Plotting Assistant create plots in Python and Matplotlib directly in your Python script or notebook.[3]

#### GPT_CodeInterpreter
GPT_CodeInterpreter is a python code interpreter implemented using OpenAI API key,with Chainlit and GPT-4.[4]

##### references
- [1][chatgpt-plugins-code-interpreter](https://openai.com/blog/chatgpt-plugins#code-interpreter)
- [2][gpt-code-ui](https://github.com/ricklamers/gpt-code-ui)
- [3][PlotAI](https://github.com/mljar/plotai)
- [4][GPT_CodeInterpreter](https://github.com/boyueluzhipeng/GPT_CodeInterpreter)
- [5][function-calling-and-other-api-updates](https://openai.com/blog/function-calling-and-other-api-updates)