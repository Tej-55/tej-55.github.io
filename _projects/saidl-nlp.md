---
layout: page
title: Code-Mixed Sentence Generation and Language Model Fine-Tuning
description: Evaluating BeRT and m-BeRT on code-mixed data
img:
importance: 4
category: work
---
[![Link to Repo](https://gist.github.com/cxmeel/0dbc95191f239b631c3874f4ccf114e2/raw/github.svg)](https://github.com/Tej-55/SAiDL-Summer-Assignment-2023-NLP)

## Overview

Machine learning has found extensive applications in various domains, including the monitoring of social media content for automatic flagging of abusive data. However, one challenge arises when dealing with "non-formal" language, often in the form of code-mixed framed sentences. These sentences, which combine multiple languages, pose difficulties for categorization using traditional machine learning models.

This project addresses the challenge of categorizing code-mixed sentences using fine-tuned language models. By generating code-mixed data with varying code-mixing indices and fine-tuning BeRT and m-BeRT models, I evaluated their performance on a standard code-mixed dataset.

## Problem Statement

In this project, I implemented a data creation strategy for generating code-mixed sentences by leveraging a standard translator from a monolingual Hindi corpus, specifically the HASOC 2019 Hindi dataset. Additionally, I created code-mixed data with various code-mixing indices (CMI), and fine-tuned pre-trained Language Models (LLMs), including BeRT and m-BeRT. The performance of these models was compared in terms of CMI versus accuracy and BeRT versus m-BeRT performance.

## Project Tasks

**Dataset Selection**: I utilized the Hindi 2019 dataset from the HASOC Dataset as our monolingual Hindi corpus. This dataset contains labeled data related to abusive content on social media platforms like Twitter.

**Code-Mixed Sentence Generation**: I employed a standard translator to generate code-mixed sentences from the monolingual Hindi corpus. The code-mixing index (CMI) was varied (CMI of _0.2_, _0.4_, _0.6_ and _0.8_) to create code-mixed data with different degrees of language mixing with _0.2_ consisting of _20%_ English and _80%_ Hindi words.

**Data Preprocessing**: Before fine-tuning the language models, I allowed the standard _cased_ Preprocessors from TensorFlow Hub to pre-process the data in each case. I used two different Preprocessors for Monolingual (English) and Multilingual models, leaving the special character _**'#'**_ in place for tokenization.

**Language Model Fine-Tuning**: I fine-tuned two pre-trained language models, BeRT and m-BeRT, using the generated code-mixed data to enhance their performance for code-mixed sentence classification.

**Performance Evaluation**: The fine-tuned models were evaluated on each of the four code-mixed datasets, measuring performance in terms of accuracy and comparing results against different code-mixing indices.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/train_accuracy_monolingual.png" title="Train Accuracy vs epochs - Monolingual BeRT Model" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/test_accuracy_monolingual.png" title="Test Accuracy vs epochs - Monolingual BeRT Model" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Monolingual BeRT Model performance: Train accuracy (left) and Test accuracy (right) vs epochs over various CMI values.
</div>

## Results

### Monolingual BeRT Model

From the graphs above, we can observe an interesting trend. As the CMI score increases, the train accuracy of the monolingual BeRT model increases gradually. This indicates that the model faces challenges in accurately predicting the code-mixed sentences with lower language mixing.

Similarly, the test accuracy of the model also exhibits mostly an increase trend as the CMI score increases. This implies that the performance of the monolingual BeRT model increases when exposed to code-mixed data with higher language mixing.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/train_accuracy_multilingual.png" title="Train Accuracy vs epochs - Multilingual BeRT Model" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/test_accuracy_multilingual.png" title="Test Accuracy vs epochs - Multilingual BeRT Model" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Multilingual BeRT Model performance: Train accuracy (left) and Test accuracy (right) vs epochs over various CMI values.
</div>

### Multilingual BeRT Model

The graphs reveal intriguing insights. Unlike the monolingual BeRT model, the train accuracy of the multilingual BeRT model remains _relatively more_ stable across different CMI scores. This suggests that the model is more resilient to code-mixed sentences with varying degrees of language mixing.

Similarly, the test accuracy of the multilingual BeRT model also remains _relatively more_ consistent as the CMI score increases. This indicates that the model can handle code-mixed data with lower language mixing more effectively compared to the monolingual BeRT model.

## Discussion

The results obtained from the experiments with both the monolingual and multilingual BeRT models provide valuable insights into their performance on code-mixed data with varying CMIs. The monolingual BeRT model demonstrates a clear increase in train and test accuracy as the CMI score increases, indicating the model's difficulty in accurately classifying sentences with lower CMI score, i.e. having more Hindi words.

On the other hand, the multilingual BeRT model exhibits greater robustness across different CMI scores. The train and test accuracies are not showing a direct behavior as they did in the case of monolingual model, implying that the multilingual model is more adaptable to code-mixed data with varying degrees of language mixing. 

We can see a huge improvement in the test accuracy in the lower CMI scores in the multilingual model. It can be because the model had more training experience in recognizing the Hindi words and, thus, it gave better results over the test datasets.

These findings suggest that incorporating multilingual capabilities in language models can enhance their ability to handle code-mixed content effectively. By leveraging a wider linguistic context, the multilingual BeRT model demonstrates improved performance on code-mixed sentences compared to the monolingual BeRT model.

## Conclusion

This project addressed the challenge of categorizing code-mixed sentences using fine-tuned language models. By generating code-mixed data with varying code-mixing indices and fine-tuning BeRT and m-BeRT models, I evaluated their performance on a standard code-mixed dataset. 

The project provided insights into the impact of language mixing on model accuracy and compared the performance of different language models. It also shed light on the advantages of using a multilingual model and explored the potential enhancements that can be achieved by leveraging a multilingual language model in real-world applications. 

The findings from this project can contribute to the development of more effective techniques for handling code-mixed content in machine learning applications, particularly in the context of social media content monitoring and abuse detection.

### Acknowledgement 
Special thanks to [SAiDL](https://www.saidl.in/) for providing the problem statement.
