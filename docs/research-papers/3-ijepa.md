---
layout: default
title: I-JEPA
parent: Research Papers
nav_order: 3
---

# I-JEPA: Image-based Joint-Embedding Predictive Architecture

**Self-Supervised Learning from Images with a Joint-Embedding Predictive Architecture** by Mahmoud Assran et al.

Image-based Joint-Embedding Predictive Architecture (I-JEPA) is a simple and efficient method for learning semantic image representations without relying on hand-crafted data augmentations. By predicting in representation space, I-JEPA converges faster than pixel reconstruction methods and learns representations of a high semantic level.

The idea behind I-JEPA is to predict missing information in an abstract representation space and pair it with a mult-block masking strategy.

## Methodology

![I-JEPA](../../../assets/research-papers/3-ijepa/img1.png)

- **Overall objective**: Given a context block, predict the representations of various target blocks in the same image.

- **Targets**: Obtained by converting an input image into a sequence of non-overlapping patches which are encoded into patch-level representations. These representations are then randomly sampled to give target blocks.

- **Context**: A block is randomly sampled from the image and any overlapping regions with target blocks are removed. This context block is encoded to give a patch-level representation of context.

- **Prediction**: Given the output of the context encoder (patch-level representation of context), the target block representations are predicted. The predictor takes the patch-level representation of context and mask tokens for each patch to be predicted as input and returns the predicted patch-level representations.

- **Loss**: The L2 distance between the predicted patch-level representations and target patch-level representations is used as the loss.

- **Optimizer**: The parameters of the predictor and context-encoder are learned through gradient-based optimization while the parameters of the target-encoder are updated via an exponential moving average of the context-encoder parameters.

## Results

- I-JEPA learns strong off-the-shelf representations without the use of hand-crafted view augmentations.

- I-JEPA is competitive with view-invariant pretraining approaches on semantic tasks and achieves better performance on low-level vision tasks. By using a simpler model with less rigid inductive bias, I-JEPA applies to a wider set of tasks.

- I-JEPA is scalable and efficient. Predicting in representation space significantly reduces the total computation needed for self-supervised pretraining.

[I-JEPA Paper](https://arxiv.org/abs/2301.08243)
[I-JEPA GitHub Repository](https://github.com/facebookresearch/ijepa)
