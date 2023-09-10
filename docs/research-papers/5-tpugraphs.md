---
layout: default
title: TpuGraphs
parent: Research Papers
nav_order: 5
---

# TpuGraphs: Performance Prediction for Tensor Programs

**✨TpuGraphs: A Performance Prediction Dataset on Large Tensor Computational Graphs✨** by Phothilimthana et al.

TpuGraphs introduces a performance prediction dataset and baseline models on tensor programs, represented as computational graphs, running on Tensor Processing Units (TPUs).

## Important Terms and Background

### Performance Prediction

- It is the task of predicting the execution time or other performance factors of a program on a given hardware.
- Models that estimate program performance are called performance models.
- Precise hardware performance models are crucial for code optimization. They can assist compilers in making heuristic decisions or aid autotuners in identifying the optimal configuration for a given program.

### Compiler

- Compilers convert programs written by humans into efficient executables for computer hardware.
- Compilers have two tasks - translation and optimization. They must translate programs into executables while also finding the most efficient translation.
- Compiler autotuning enables compilers to find the optimal configuration of programs with minimal or no interaction from a user.
- While solving optimization problems, compilers often use performance models to estimate performance instead of collecting performance measurements from real hardware. The latter can be expensive, limited or infeasible.
- Machine Learning (ML) compilers solve multiple optimization problems to translate an ML program, represented as a tensor computation graph, to an efficient executable for hardware targets.

### XLA (Accelerated Linear Algebra)

- It is a domain-specific production-grade heuristics-based compiler for ML programs (Linear Algebra) capable of generating code for various hardware targets, including CPUs, GPUs, and TPUs.
- In XLA, tensor computation graphs are High-Level Operations (HLO). Each optimization pass transforms an HLO graph into a functionally equivalent one.
- XLA has an autotuner that can tune both graph-level and kernel-level configurations for TPUs.

### Kernel-Level Optimizations

- Kernel-level optimizations require only the context of each kernel while making optimization decisions.
- Each node in a tensor computation graph is a tensor operation. A kernel, represented as a fused subgraph, is a fusion of multiple tensor operations.
- A crucial optimization at the kernel level is the tile size selection. Tile size selection deals with selecting the shape of a tile of the output tensor to maximize the compute efficiency of the hardware.

### Graph-Level Optimizations

- Graph-level optimizations require the context of the entire program graph to make good decisions.
- The graph-level optimizations supported by the XLA autotuner include layout assignment, fusion, and memory space assignment passes. It supports compiler flags that control multiple optimization passes.

![Important Optimizations in ML Compilers](../../../assets/research-papers/5-tpugraphs/img1.png)

## Dataset

- TpuGraphs is a performance prediction dataset on tensor programs representing the computation of an ML program (one or many training steps or one inference step) as computational graphs.
- The data is split into training, validation and test sets using an 80-10-10 ratio by graphs in each collection.

### Data Sample

- Each data sample contains the following:
  - HLO Computation Graph
  - Configuration of TPU v3
  - Execution time on single-core TPU v3
- The compilation configuration controls how the XLA compiler transforms the graph for a specific optimization pass.
- The HLO graph in each data point is optimized partially before being fed into the corresponding optimization pass. That is:
  - For the layout collection, an HLO graph is the input graph to the layout assignment pass. The layout configuration is a collection of per-node layout decisions on configurable nodes.
  - For the tile collection, an HLO graph in each data point is a fused subgraph representing a kernel. The tile configuration is the configuration of the entire subgraph, not specific to any particular node.

### Collections

- TpuGraphs has the following collections:
  - Layout Configurations: control how the tensors are laid out in the physical memory by specifying the dimension order of each input and output of an operation node.
  - Tile Configurations: control the tile size of each subgraph.
- The dataset primarily focuses on layout and tile configurations as tuning them offers the highest performance gain on average, compared to tuning other compiler optimizations.

### Data Generation

- The HLO Graphs:
  - XLA Source: a combination of XLA regression benchmark and MLPerf benchmark.
  - NLP Source: Various BERT for training and inference, with varying layers, attention heads, and hidden sizes. The largest XLA compiled graph is collected for each model.
- The Configurations:
  - The XLA autotuner generates data samples from the graphs.
  - For layout collections:
    - Default mode:
      - The autotuner explores the search space using a genetic algorithm starting from the default configuration, chosen by the compiler's heuristic.
      - Configurations from this mode are not too different from the default and have similar execution times.
    - Random mode:
      - The autotuner explores the search space by picking random candidates.
      - Configurations from this mode are very different and have different execution times.
  - For tile collections:
    - The autotuner invokes the compiler to run the graph-level optimizations and obtain fused subgraphs (kernels).
    - For each subgraph, the autotuner enumerates all the possible tile sizes for the kernel in random order (limited by time out) as the tile size search space is much smaller.

### Feature Extraction

- TpuGraphs provides data in raw protobuf format and numpy arrays similar to OGBG format.
- The autotuner produces output results in protobuf format that get converted to numpy arrays using a data pre-processing script.
- The feature extraction function works as follows:
  - Node feature vectors (describe node's properties) are extracted by copying values from various fields in HLO instruction (a node in HLO graph) as they are or converting categorical values using one-hot encoding.
  - An unbounded list of numbers is converted to a fixed-size vector by truncating the list to six elements and including the summation and/or product of all the elements in the list.
  - Per-node layout configuration and tile size are represented as a nested list with some unbounded dimensions truncated to six elements.

![TpuGrpahs Dataset Statistics](../../../assets/research-papers/5-tpugraphs/img2.png)

## Insights

Experiments with baseline models on TpuGraphs provide the following insights that can improve performance in future iterations of the models:

- Layout Collection:
  - Layout:XLA: Random and Layout:NLP: Random are the most difficult collections.
  - The Graph Segment Training (GST) Method significantly improves the model quality over full graph training.
  - The model quality drops when the graph segment size is too small.
  - Using fewer Graph Neural Network (GNN) layers doesn't affect accuracy significantly.
  - The choice of partition algorithm (METIS or Topo Partition) does not matter much.
  - Pairwise Hinge Loss is significantly better as a loss function than Mean Squared Error (MSE).
- Tile Collection:
  - Combining configuration features with node features earlier (early join) is superior to combining configuration features with a reduced graph embedding later (late join).
  - Using a ranking loss (ListMLE) is more effective than using MSE.
  - GraphSAGE is a better choice for GNN than GCN.
  - GNN is essential for good accuracy (better performance than LSTM & Transformer based on previous work).

## Directions to Explore

- Tensor computation graph typically contains repeated subgraphs, representing reported blocks of neural network layers. This repeated structure can be leveraged to devise a more compact representation that is easier to learn.
- The dataset may contain some types of graphs significantly more than others. The data imbalance can be addressed to improve the quality of the learned model.
- Use analytical modelling when easy to do and use the learned model to make corrections to the analytical estimates.
- Different feature extraction methods.

## For more information

- [📜Paper](https://arxiv.org/abs/2308.13490)
- [⭐GitHub](https://github.com/google-research-datasets/tpu_graphs)
