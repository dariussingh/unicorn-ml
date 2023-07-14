---
layout: default
title: Segment Anything
parent: Research Papers
nav_order: 1
---

# Segment Anything!

Segment Anything by Alexander Kirillov et al. (Meta AI Research, FAIR) proposes a new task, model and dataset for image segmentation.

The goal of the Segment Anything project is to build a foundational model for image segmentation that solves a range of downstream segmentation problems on new data distributions using prompt engineering.

![Main components of Segment Anything](../../../assets/research-papers/1-segment-anything/img1.png)

The main components of the project are:

- **Task**: A promptable segmentation task, where the objective is to return a valid segmentation mask given any segmentation prompt. Where valid implies that the masks are reasonable even for ambiguous prompts and a segmentation prompt is foreground/background points, a rough box, a mask, free-from text or any information indicating what needs to be segmented in the image.
- **Model**: The Segment Anything Model (SAM) supports flexible prompts, computes masks in amortized real-time and is ambiguity-aware. SAM consists of a powerful image encoder that computes image embedding, a prompt encoder that embeds prompts and a lightweight mask decoder that combines the two information sources and predicts segmentation masks.
- **Data**: SA-1B dataset that includes 1B masks from 11M licensed and privacy-preserving images that were collected using a data engine. The Segment Anything Data Engine has three stages: 1) The assisted-manual stage where SAM assists annotators in annotating masks, 2) the semi-automatic stage where SAM automatically generates masks and annotators focus on annotating the remaining objects, and 3) the fully automatic stage where SAM is prompted with a regular grid for points and it automatically generates masks of the image.

Results show, competitive to state-of-the-art performance by SAM (zero-shot) in single-point segmentation, edge detection, object proposal generation, instance segmentation and free-form text segmentation. Hence SAM, with its generality and breadth of use, has shown the potential to be worthy of the status of a foundational model for image segmentation.

Limitations of SAM include its inability to segment fine structure and hallucination with small disconnected components. SAM can process prompts in real-time, but its overall performance is not real-time as it uses a heavy image encoder.

The Segment Anything Project has built a solid foundation for further innovation in image segmentation allowing SAM to be a component of a larger system.

<video width="100%" src="../../../assets/research-papers/1-segment-anything/vid1.mp4" controls title="SAM demo"></video>

What are some use cases and further research directions that can be taken with the help of the Segment Anything Project? Let’s continue the conversation in the comments section and learn from each other.

[Segment Anything Demo](https://segment-anything.com/)

[The Segment Anything research paper](https://ai.facebook.com/research/publications/segment-anything/)
