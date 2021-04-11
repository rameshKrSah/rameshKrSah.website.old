---
title: "Debugging Machine Learning Models"
date: 2021-02-29
comments: True
mathjax: True
tags: [machine learning]
categories:
  - machine learning
---

Some practical tips on debugging machine learning models.

1. First determine what the algorithm can learn and not learn. For this first train the algorithm on a small subsample of your dataset. If you can overfit the model on this dataset, then the algorithm is able to learn and you can move on to training on the complete dataset.

2. Figure out how we can help the model learn faster and better. By better, I mean low generalization error. Look at the learning curves, monitor the gradient update ratios (for neural networks), and tune hyperparameters.

3. Determine whether the model is learning what you meant it to learn. Periodically check your model's predictions, visualize the learned representation, check different errors, use different evaluation metrics, and add noise to the data to check the generalizability.