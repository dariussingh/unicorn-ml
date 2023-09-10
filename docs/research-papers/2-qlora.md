---
layout: default
title: QLoRA
parent: Research Papers
nav_order: 2
---

# QLoRA: A new way to finetune LLMs

**QLoRA: Efficient Finetuning of Quantized LLMs** by Tim Dettmers, Artidoro Pagnoni, Ari Holtzman and Luke Zettlemoyer.

**QLoRA** is an efficient finetuning approach that reduces memory usage enough to finetune a 65B parameter model on a single 48GB GPU while preserving full 16-bit finetuning task performance. QLoRA backpropagates gradients through a frozen, 4-bit quantized pre-trained language model into Low-Rank Adapters (LoRA).

![Different finetuning methods](../../../assets/research-papers/2-qlora/img1.png)

## Innovations

QLoRA introduces the following innovations to reduce memory usage without sacrificing performance:

1. **4-bit NormalFloat (NF4)**:

   - An information-theoretically optimal quantization data type for normally distributed data.
   - The NF is built on Quantile Quantization (IT optimal data type) and estimated (asymmetrically) using SRAM quantiles (quantile approximation algorithm) on the zero-mean normal distribution of weights of the pre-trained neural network.

2. **Double Quantization (DQ)**:

   - A method that quantizes the quantization constraints saving additional memory (approx. 3 GB for a 65B model).
   - DQ symmetrical quantizes the 32-bit Floating Point (FP32) quantization constants of the first quantization into 8-bit Floating Point (FP8) quantized quantization constants.

3. **Paged Optimizers:**

   - Manage memory spikes during gradient checkpointing and prevent out-of-memory errors.
   - Done by allocating paged memory for the optimizer states which are then automatically evicted to CPU RAM when the GPU runs out of memory and paged back into GPU memory when the memory is needed in the optimizer update step.

## Key Insights

Key insights from experiments:

1. 4-bit QLoRA with NF4 data type matches 16-bit full finetuning and 16-bit LoRA finetuning performance on academic benchmarks.
2. NF4 is more effective than FP4 and double quantization does not degrade performance.
3. With a given finetuning and inference resource budget it is beneficial to increase the number of parameters in the base model while decreasing their precision.
4. Finetuning on a small high-quality dataset leads to state-of-the-art results, even when using smaller models than previous SoTA (data quality is far more important than data size).
5. GPT-4 model-based evaluation can be used as a cheap alternative to human annotation but has some biases (strong order effects and bias in favour of its output).
6. Current benchmarks are not trustworthy to accurately evaluate performance (dataset suitability matters more than size for a given task).
7. The most critical LoRA hyperparameter is how many LoRA adapters are used in total.

[QLoRA Research Paper](https://arxiv.org/abs/2305.14314)

[QLoRA GitHub Repository](https://github.com/artidoro/qlora)
