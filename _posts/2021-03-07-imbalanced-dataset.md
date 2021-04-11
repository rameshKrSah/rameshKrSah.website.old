---
title: "Dealing with Imbalanced Datasets"
date: 2021-03-07
comments: True
mathjax: True
tags: [machine learning]
categories:
  - machine learning
---

In machine learning often, we often have imbalanced datasets. There are many ways to deal with imbalanced datasets and we 
below I list the most important things to take into account when dealing with imbalanced datasets.

1. Use proper evaluation metrics: Precision-Recall Curve, ROC Curve.
2. Predict class probabilities, not the labels.
3. Oversampling of the minority class and undersampling of the majority class.
4. Use ensembles techniques such as bagging and majority voting.
5. Adjust class weights and loss functions.
6. Use proper loss functions such as log-loss and focal loss.

A detailed description of these methods can be found [here](http://www.svds.com/learning-imbalanced-classes/).
