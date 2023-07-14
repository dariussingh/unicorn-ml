---
layout: default
title: LLM-Blender
parent: Research Papers
nav_order: 4
---

# Ensemble LLMs with LLM-Blender

**✨ LLM-Blender: Ensembing Large Language Models with Pairwise Ranking and Generative Fusion ✨**
by Dongfu Jiang, Xiang Ren and Bill Yuchen Lin.

LLM-Blender is an ensembling framework designed to attain consistently superior performance by leveraging the diverse strengths of multiple open-source large language models (LLMs).

## Is there a need for LLM ensembling?

![Motivation of ensembling LLMs](../../../assets/research-papers/4-llm-blender/img1.png)

- Open-source LLMs exhibit diverse strengths and weaknesses due to variations in data, architectures and hyperparameters, making them complementary.

- There does not exist one open-source LLM that dominates the competition for all examples.

- There is a need to ensemble the output of the best LLMs (based on input, task and domain) to give consistently superior performance across examples.

- By combining their unique contributions; the biases, errors and uncertainties in individual LLMs can be alleviated, resulting in outputs aligned with human preferences.

## How does LLM-Blender ensemble LLMs?

![The LLM-Blender Framework](../../../assets/research-papers/4-llm-blender/img2.png)

LLM-Blender achieves consistently superior performance by mixing the outputs of multiple LLMs. It has two modules: PairRanker and GenFuser. Initially, PairRanker compares the outputs from multiple LLMs to give the top-ranked outputs. The first few top-ranked outputs are then fused by GenFuser to generate a final output that combines their advantages and mitigates their shortcomings.

## How does PairRanker work?

- The PairRanker module is used to effectively discern subtle differences between candidate (LLM) outputs and rank them based on their quality.

- Outputs from N models are gathered and paired in a total of N(N-1)/2 ways (number of combinations where 2 items are selected from a total of N items).

- These pairs are then evaluated on the condition: given the input prompt which candidate’s output is better.

- During inference, a matrix containing logits representing pairwise comparison results is computed. And given this matrix, the top K-ranked outputs are determined and selected for the GenFuser module.

## How does GenFuser work?

- The GenFuser module uses the top-ranked outputs by the PairRanker module to generate a potentially improved output for the end-users.

- The module fuses the top K of the N-ranked candidates and generates an improved output capitalising on their strengths and mitigating their weaknesses.

## What is the dataset used to benchmark results?

- A new dataset called the MixInstruct, to benchmark ensemble models for LLMs in instruction-following tasks is introduced.

- The dataset has a large-scale set of instruction examples from Alpaca-GPT4, Dolly-15K, GPT4-ALL-LAION and ShareGPT.

- There are 100k examples for training, 5k for validation, and 5k for testing.

- N = 11 popular open-source LLMs are prompted to give output on the dataset. The outputs of the candidate LLMs are evaluated using ChatGPT for all candidate pairs (55 pairs). For each pair, ChatGPT is asked to judge the better candidate (or declare a tie).

## What are the results from benchmarking on MixInstruct?

![The LLM-Blender Framework](../../../assets/research-papers/4-llm-blender/img3.png)

- LLMs have diverse strengths and weaknesses.

- Top LLMs are not always good.

- PairRanker outperforms other LLM rankers.

- LLM-Blender ensembling beats top individual models.

## What are the limitations of LLM-Blender?

- **Efficiency**: The process of ranking the top-K outputs in PairRanker needs to call the model O(n²) times to get optimal performance. A way around this is using multiple rounds of bubble-sort methods to reduce the number of inferences needed. Another way to improve time efficiency is to execute inferences for the PairRanker in parallel as they are independent.

- **Human evaluation**: The benchmark and results use automatic evaluation with the help of ChatGPT. While automatic evaluation is a good alternative, human evaluation could provide more reliable and comprehensive evaluation results.

## For more information

- A simplified explanation of LLM-Blender:

<iframe
  src="https://www.youtube.com/embed/zyQHtWFLNxY"
  title="LLM-Blender"
  style="width:100%; aspect-ratio: 1.77;"
></iframe>

- [📜Paper](https://arxiv.org/abs/2306.02561)

- [⭐GitHub](https://github.com/yuchenlin/LLM-Blender)
