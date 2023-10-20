---
layout: post
title: "modelstore - Filesystem or Cloud Storage as Model Registry"
date:   2023-10-20
tags: [tech, MLOps]
comments: true
author: GingerNg
---

### MLOps
MLOps(Machine Learning Operations) is a practice that focuses on the deployment, management, and monitoring of machine learning models in production environments. It combines principles from software engineering, data science, and DevOps to ensure the smooth and efficient operation of machine learning systems.

The main goal of MLOps is to bridge the gap between the development and deployment of machine learning models by establishing robust and scalable processes. This involves automating the various stages of the machine learning lifecycle, including data preprocessing, model training, evaluation, deployment, and monitoring.

By implementing MLOps practices, organizations can improve the reliability, scalability, and maintainability of their machine learning systems. This includes version control for models and data, reproducibility of experiments, automated testing, continuous integration and deployment, and effective monitoring and alerting mechanisms.
The infrastructure below shows Amazon Sagemaker MLOps consisting of Exeriment, Model training, Model registry, CI/CD, Model deployment and Monitoring.
![Amazon SageMaker MLOps](https://github.com/GingerNg/gingerng.github.io/blob/master/images/sagemaker%20MILOps.png?raw=true)

### Model Registry
This post focuses on model registry which also known as a model management system or artifact repository, is a tool or platform that helps organizations manage and track their machine learning models throughout their lifecycle. It provides a centralized location to store, version control, and organize trained models, as well as metadata associated with the models.

There is a difference between model repository and model registry. Model Repository is a storage location for machine learning models, while a Model Registry is a more comprehensive system that tracks and manages the full lifecycle of machine learning models.[2]

There may be different understarding of model registry between different systems or companies. Neptune thinks model registry has to integrate with the Experiment management system (which tracks the experiments) to register ML models from various experiment runs to make them easier to find and work with.[2] While, in Amazon Sagemaker MLOps, model registry is aimed to centrally catalog and manage trained models separated from Experiments component.

### modelstore
Commerical MLOps Saas such as Neptune[2] or Wandb[4] have built-in model registry, however, maybe is expensive or limited. This post introduced modelstore[3] a easy-use tool to let you have a free model registry without a tracing server like MLflow[5]. The modelstore is a Python library that allows you to version, export, and save a machine learning model to your filesystem or a cloud storage provider. For example, if you are user of Amazon S3 and have some training scripts. You only have to modify the part of saving and loading model in your code. Also, modelstore has support most ML/DL frameworks/libraries. If there are some frameworks/libraries unsupported, just use the raw file interface.
Could storage is used as as model registry in Monzo’s machine learning stack[6]:
![Monzo’s machine learning stack](https://images.ctfassets.net/ro61k101ee59/5PFHY5F9SzWGOSuc2zjMgM/d7af54b185d9a05d56acb498fd6c6df0/Screenshot_2022-04-04_at_10.09.56.png?w=656&q=90)

- [1][aws-sagemaker-mlops](https://aws.amazon.com/cn/sagemaker/mlops/)
- [2][ML Model Registry: The Ultimate Guide](https://neptune.ai/blog/ml-model-registry)
- [3][modelstore](https://github.com/operatorai/modelstore)
- [4][wandb](https://docs.wandb.ai/guides/model_registry)
- [5][AMA with Neal Lathia: data science career tracks, shipping ML models to production, and Monzo ML stack](https://www.evidentlyai.com/blog/ama-neal-lathia)
- [6][Monzo’s machine learning stack](https://monzo.com/blog/2022/04/26/monzos-machine-learning-stack)