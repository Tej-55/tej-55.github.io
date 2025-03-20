---
layout: page
title: Variations of Softmax
description: Exploring different softmax implementations for neural networks
img:
importance: 5
category: work
---
[![Link to Repo](https://gist.github.com/cxmeel/0dbc95191f239b631c3874f4ccf114e2/raw/github.svg)](https://github.com/Tej-55/SAiDL-Summer-Assignment-2023-Core_ML)

# Variations of Softmax

The softmax function is a cornerstone activation function in neural networks, particularly for classification tasks. It transforms a vector of K real numbers into a probability distribution of K possible outcomes, enabling neural networks to map probabilistic distributions. However, as the number of classes increases, the computational cost of the standard softmax function can become prohibitive, leading to slower training and evaluation times.

## Problem Statement

This project explores different variations of softmax implementations in neural networks and evaluates their impact on model performance and training time. I developed a convolutional neural network (CNN) model on the CIFAR 100 dataset for image classification and compared the standard softmax implementation with alternative softmax functions designed to reduce computational complexity.

## Project Tasks

### Dataset
I used the CIFAR 100 dataset, which consists of 60,000 32x32 color images across 100 classes. The dataset is divided into 50,000 training images and 10,000 test images, providing a challenging multi-class classification problem.

### Model Development
I designed a CNN architecture specifically for image classification. The initial model used the standard softmax implementation as the activation function for the output layer.

### Alternative Softmax Implementations
I created a second model with identical architecture but implemented different softmax variations to reduce computational complexity. The alternatives included:

- **Gumbel-Softmax**: A differentiable approximation of the argmax function that allows for efficient gradient computation
- **Hierarchical Softmax**: A method that organizes classes in a tree structure to reduce computation (implementation attempted but faced training issues)

Each implementation was analyzed for its time complexity and practical performance impact.

### Performance Evaluation
I evaluated both models using comprehensive metrics:
- Accuracy
- Precision
- Recall
- F1 score
- Confusion matrix

This thorough evaluation allowed for meaningful comparison between different softmax implementations.

## Results and Findings

The experimental results revealed interesting trade-offs between model accuracy and computational efficiency:

- **Regular Softmax**: Achieved slightly better performance metrics with an F1 score of 0.3802
- **Gumbel Softmax**: Achieved an F1 score of 0.3781, slightly lower than regular softmax

However, the training time comparison showed significant differences:
- **Regular Softmax**: Mean epoch time of 6.487 seconds
- **Gumbel Softmax**: Mean epoch time of 5.845 seconds

Both implementations have the same theoretical time complexity of O(n) with respect to the number of classes. However, Gumbel Softmax demonstrated faster practical performance during training due to its reparameterization trick, which enables more efficient gradient computation and backpropagation.


## Conclusion

This project provides valuable insights into the trade-offs between different softmax implementations in neural networks, particularly for classification tasks with numerous classes. While the standard softmax implementation achieved marginally better performance metrics, the Gumbel Softmax demonstrated significant computational efficiency advantages with only a slight decrease in accuracy.

These findings are particularly relevant for applications where training time is a critical factor, such as large-scale image classification systems or real-time applications. The Gumbel Softmax, with its reparameterization trick, offers an attractive alternative for models that involve discrete decisions, including reinforcement learning agents with discrete action spaces.

### Acknowledgement 
Special thanks to [SAiDL](https://www.saidl.in/) for providing the problem statement.

