# Early Checkpoints

This folder contains earlier notebooks and intermediate milestones from the development of the XAI workflow. They are kept mainly for traceability, retrospective lookup, and as proof of the work path that led to the current version.

These are internal workflow files, so most of them do not contain much extra explanation inside. In other words: this folder is more useful as a development archive than as a polished guide `(^///^)`

## File index

- [`embeddingExploration.ipynb`](./embeddingExploration.ipynb)  
  Early exploration of embedding structure, consistency, and distribution. This work later helped with notebook automation and with separating different parts of the meta-embeddings so importance values could be assigned to individual model components.

- [`exploratoryDataAnalysis.ipynb`](./exploratoryDataAnalysis.ipynb)  
  Exploratory analysis of the available data, training pipelines from earlier stages of the work and of the embeddings obtained during model training. This notebook helped identify consistency issues and supported the preparation of a clean test set for later experiments.

- [`modelWorkflow.ipynb`](./modelWorkflow.ipynb)  
  Early working notebook that connected the main parts of the pipeline needed for predictions: model loading, data loading, classifier loading, and execution. In practice, this was the first notebook that made prediction-based explanation experiments actually possible within the original project structure.

- [`/nb_embedding_diagnostics_standalone.ipynb`](.//nb_embedding_diagnostics_standalone.ipynb)  
  AI-generated diagnostic notebook intended to explore whether mean and median embeddings make sense as references for ablation tests. It is a bit messy and not central to the final workflow, but it may still be interesting for someone who wants to revisit that direction.

- [`nb1_kernel_explainer(early.ver).ipynb`](./nb1_kernel_explainer(early.ver).ipynb)  
  Early development version of the KernelSHAP workflow. This is basically the first working prototype before later cleanup, comments, and late-stage adjustments; it was kept mostly as a backup in case something broke during annotation or refinement.

- [`nb2_two_level_hierarchy(early.ver).ipynb`](./nb2_two_level_hierarchy(early.ver).ipynb)  
  Early development version of the hierarchical explanation workflow. Same idea as above: an older saved state that may miss some later improvements, but still documents an important stage of the development cycle.