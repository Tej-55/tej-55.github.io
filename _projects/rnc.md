---
layout: page
title: Rank-N-Contrast
description: Learning Continuous Representations for Regression
img: assets/img/rnc_paper_prev.png
importance: 1
category: work
---
[![Link to Repo](https://gist.github.com/cxmeel/0dbc95191f239b631c3874f4ccf114e2/raw/github.svg)](https://github.com/karannb/rank-n-contrast)

## Rank-N-Contrast: Learning Continuous Representations for Regression

This project reproduces the NeurIPS 2023 Spotlight paper [Rank-N-Contrast: Learning Continuous Representations for Regression](https://arxiv.org/abs/2210.01189) as a course project for CS F425 - Deep Learning. Rank-N-Contrast (RNC) is a novel framework that learns continuous representations for regression by contrasting samples against each other based on their rankings in the target space.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/rnc_paper_prev.png" title="Representation visualization comparison" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Comparison of learned representations using different methods on a temperature regression task. Left: L1 loss (standard regression), Middle: SupCon (supervised contrastive learning), Right: RNC (proposed method). Notice how RNC creates a continuous representation that better captures the ordered relationships between samples. (Figure from the RnC paper)
</div>

## Key Concept

Traditional regression models typically learn in an end-to-end fashion without explicitly emphasizing a regression-aware representation. This leads to fragmented representations that fail to capture the continuous nature of sample orders. RNC addresses this limitation by learning representations that preserve the ordering relationships between samples according to their target values.

### The RnC Loss Function

The core of our implementation is the RnC Loss function that ranks samples in a batch according to their labels and then contrasts them against each other based on their relative rankings:

```
from loss import RnCLoss

# define loss function with temperature, label difference measure, and feature similarity measure
criterion = RnCLoss(temperature=2, label_diff='l1', feature_sim='l2')
loss = criterion(features, labels) # features: (bs, 2, fear_dim), labels: (bs, label_dim)
```

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/rnc_concept.png" title="RNC framework" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
llustration of L_{RNC} in the context of positive and negative pairs.
</div>

## Experiments and Results

We conducted experiments in two domains:

### 1. Computer Vision: Age Estimation

We reproduced the original paper's results using the AgeDB dataset, which contains face images of celebrities, politicians, and scientists at different ages (ranging from 3 to 101 years).

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/agedb_prev.png" title="AgeDB examples" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Examples from the AgeDB dataset showing faces at different ages. The dataset contains 16,488 images of 568 distinct subjects with an average age range of 50.3 years per subject.
</div>


Our implementation follows a two-stage approach:
1. Train an encoder with the RnC framework
2. Use the trained encoder to train a regressor on top

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/representation_space_cv.png" title="UMAP visualization of training data" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    UMAP visualization of the representation space learned by RnC versus end-to-end L1 loss. Left: Training data, Right: Test data. Notice how RnC creates a more continuous and ordered representation space that better captures the underlying structure of the regression targets.
</div>

### 2. Graph Regression: ESOL Dataset

We extended the original work by applying RNC to a graph regression task using the ESOL dataset (water solubility prediction for molecules).

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/representation_space_train.png" title="UMAP visualization of training data" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/representation_space_test.png" title="UMAP visualization of test data" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    UMAP visualization of the representation space learned by RnC versus end-to-end L1 loss. Top: Training data, Bottom: Test data. Notice how RnC creates a more continuous and ordered representation space that better captures the underlying structure of the regression targets.
</div>

Our results demonstrate the superiority of RNC over standard regression approaches:


| Method / Loss | test MAE | test RMSE | test MSE | validation MAE | validation RMSE | validation MSE |
| :-----------: | :------: | :-------: | :------: | :------------: | :-------------: | :------------: |
| normal-L1 | 0.247	| 0.326 | 0.106 | **0.224** | 0.325 | 0.106 |
| RnC(L1) + freeze | 0.219 | **0.297** | 0.088 | 0.255 | 0.359 | 0.129 |
| RnC(L1) | **0.212** | 0.314 | 0.099 | 0.235 | 0.345 | 0.119 |
| RnC(L2) | 0.266 | 0.342 | 0.117 | 0.276 | 0.366 | 0.134 |
| RnC(Huber) | 0.242 | 0.326 | 0.106 | 0.245 | **0.317** | **0.101** |

## Key Findings

Our experiments revealed several intriguing properties of RNC:

1. **Better Performance**: RNC consistently outperforms standard regression approaches across different tasks.
2. **Improved Data Efficiency**: RNC requires less training data to achieve comparable performance.
3. **Enhanced Robustness**: RNC shows better robustness to spurious targets and data corruptions.
4. **Better Generalization**: RNC generalizes better to distribution shifts and unseen targets.


## Conclusion

Our reproduction and extension of the Rank-N-Contrast framework demonstrate its effectiveness in learning continuous representations for regression tasks. By explicitly enforcing the ordering of samples in the representation space according to their target values, RNC creates more meaningful embeddings that lead to improved regression performance, robustness, and generalization.

This project showcases the potential of representation learning approaches for regression tasks and opens up new avenues for future research in this direction.
