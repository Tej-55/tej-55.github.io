---
layout: page
title: TITANS for Squared Amplitude Calculation
description: Implementing Google's Titans architecture for particle physics calculations
img: assets/img/titans_front.jpeg
importance: 1
category: work
---
[![Link to Repo](https://gist.github.com/cxmeel/0dbc95191f239b631c3874f4ccf114e2/raw/github-icon.svg)](https://github.com/Tej-55/TITANS-SqAmp-Calculation)

## Project Overview

In particle physics, squared amplitudes are crucial for calculating cross-sections, which provide a testable link between theory and experiment. This project explores how modern transformer architectures can learn to map from amplitudes to their squared forms using sequence-to-sequence modeling.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets\img\feynman_dia.png" title="Feynman diagram representation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A typical Feynman diagram showing particle interactions.
</div>

This repository implements and evaluates the Memory As Context (MAC) Transformer architecture from Google's [Titans: Learning to Memorize at Test Time](https://arxiv.org/pdf/2501.00663) paper for calculating squared amplitudes in particle physics. The project compares the performance of a standard T5 transformer model against the more advanced TITANS architecture on this specialized task.

## The TITANS Architecture

The TITANS architecture represents a significant advancement in how AI models handle memory. Unlike traditional transformers that struggle with long-term dependencies, TITANS introduces three distinct memory modules:

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets\img\titans_arch.jpeg" title="TITANS MAC architecture diagram" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Memory as Context (MAC) architecture showing how persistent memory, core processing, and contextual memory interact to enhance model performance.
</div>

### Memory Components

1. **Core Module**: Handles the main data processing, capturing short-term dependencies using attention mechanisms similar to traditional Transformers.

2. **Long-term Memory Module**: Stores and retrieves historical information, allowing the model to access relevant past data when processing new inputs.

3. **Persistent Memory Module**: Contains learnable, data-independent parameters that capture task-specific knowledge, providing a stable foundation for processing.

For our implementation, we focused on the Memory as Context (MAC) variant, which treats memory as contextual information for current processing. This approach has shown particular promise for complex sequence transformation tasks like our squared amplitude calculations.

## Dataset and Preprocessing

The dataset consists of particle physics expressions in the format:
```
"event type : Feynman diagram : amplitude : squared amplitude"
```


### Index Normalization

One of the key preprocessing steps involves normalizing indices in the physics expressions to reduce vocabulary size and improve model training efficiency. We use regular expressions to identify and standardize different types of indices:

1. **Momentum indices**: Patterns like `i_36289`, `j_5`, `k_3`, normalized to sequential small indices.
2. **Variable indices**: Expressions like `%sigma_157721` or `%gam_166722`, excluding momentum indices.
3. **Compound indices**: Complex identifiers with multiple parts like `gamma_gam_166722`.

This normalization process maintains consistency across expressions while significantly reducing the complexity of the input space.

## Models Implemented

### 1. T5 Transformer (Baseline)

We implemented a standard encoder-decoder transformer model using Google's [T5 Small](https://huggingface.co/google-t5/t5-small) architecture as our baseline. This well-established model provides a good reference point for evaluating the performance of our TITANS implementation.

### 2. MAC TITANS Model

Our implementation of the Memory As Context Transformer architecture includes:
- Neural memory components for enhanced pattern recognition
- Segmented attention for handling long sequences
- Adaptive memory updates for learning complex transformations

## Results

The results demonstrate a significant performance advantage for the TITANS architecture over the baseline T5 model in this specialized physics task.

### Performance Comparison

| Model | Test Sequence Accuracy | Test Token Accuracy |
|-------|------------------------|---------------------|
| T5 Transformer | 5.14% | 33.66% |
| MAC TITANS | 40.23% | 60.28% |


### Training Curves

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets\img\tp1.png" title="T5 Training Loss" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets\img\tp2.png" title="TITANS Training Loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Training loss curves for T5 (left) and TITANS (right) models, showing how loss decreases over training epochs. Note the faster convergence and lower final loss of the TITANS model.
</div>

The training curves reveal that the TITANS model not only achieves better final performance but also demonstrates more efficient learning, with faster convergence and more stable training dynamics.


## Future Work

Future directions for this project include:

1. Scaling and tuning the model to handle more complex physics expressions
2. Exploring other TITANS variants (Memory as Gate, Memory as Layer) for this task
3. Extending the approach to other datasets problems

## Acknowledgements

This code is adapted from the following sources:
- TITANS-PyTorch by lucidrains: [https://github.com/lucidrains/titans-pytorch](https://github.com/lucidrains/titans-pytorch)
- Skanformer by Riteshbhalerao11: [https://github.com/Riteshbhalerao11/Skanformer](https://github.com/Riteshbhalerao11/Skanformer)

The project was developed as part of the Google Summer of Code application for the "TITANS for squared amplitude calculation" project.