---
title: "Self-Supervised Learning for Time Series Data"
date: 2021-04-21
comments: True
mathjax: True
tags: [machine learning, SSL]
---

In domains where it is hard to get labeled data or limited labeled data such as health care, self-supervised learning lends itself as the most useful and practical machine learning paradigm. In self-supervised learning, machine learning algorithms learn the representation of the data by solving pretext tasks.

Pretext tasks are carefully designed classification or regression problems such that the machine learning model learns useful features and representation from the unlabeled data. These learned representations then can be used in downstream tasks to solve the original problem.

Given a problem \\(P\\) and corresponding dataset \\(D\\) we want to solve \\(P\\) using machine learning. Since \\(D\\) is not labeled or only a few labels are available we cannot use supervised learning. We then design some pretext tasks \\(T\\) using the dataset \\(D\\) such that we get input-output pairs from \\(D\\) i.e., \\((x_{t_i}, y_{t_i}) \in D\\) where \\(t_i\\) is the ith pretext task in \\(T\\). Next, we train machine learning models to solve the pretext tasks and then use the representation learned by the models to solve the original problem \\(P\\). This can be done using transfer learning.

Now the main part becomes coming up with these pretext tasks and answering how to design these pretext tasks. Generally, pretext tasks are designed using the principle of Contrastive Predictive Coding.

## Contrastive Methods
Contrastive methods are based on the idea of constructing pairs of \\(x_1\\) and \\(x_2\\) that are not similar to each other and learning to quantify or measure their similarity. Basically, given an input \\(x\\) we create samples \\((x_i, x_j)\\) from \\(x\\) using various strategies and then label these samples to create a dataset. The goal of this process is that by learning to quantify or measure the similarity between the created samples, the model will learn the general representation of the original  data. Contrastive methods usually employ an encoder framework to learn the representation of the data.  After learning the pretext tasks, the learned encoder is frozen and augmented with new layers for downstream tasks.

## Pretext tasks for time series data. 
My interest in self-supervised learning originated from my struggle to train a stress classification model from limited sensor data. Below I have listed some pretext tasks that can be used for self-supervised learning with time-series data.

1. Temporal cut: a random contiguous section of the time-series signal is replaced with zero

2. Temporal delays: the time-series data is randomly delayed in time.

3. Noise: independent and identically distributed Gaussian noise is added to the signal

4. Bandstop filtering: the signal content at a randomly selected frequency band is filtered out using a bandstop filter.

5. Signal mixing: another time instance or subject data is added to the signal to simulate correlated noise.

6. Relative positioning: segments are displaced along time scale and labels are created based on whether two-time segments are closed together or farther apart.

7. Temporal Shuffling: create three segments and the label is determined based on their relative ordering.

8. Blend Detection: detecting input blending as a multi-class classification problem.

9. Fusion Magnitude Prediction: predicting the magnitude which defines the blending as a regression problem.

10. Feature Prediction from Masked Window: approximate summary statistics of a masked temporal segment within a signal using a multi-head network and Huber Loss.

11. Transformation Recognition: multi-class classification problem to learn a network that can directly recognize the applied transformation on input from one out of k classes.

12. Temporal Shift Prediction: estimate the number of steps by which the samples are circularly shifted in their temporal dimension.

13. Modality Denoising: decompose a signal for obtaining a clean target through input reconstruction, i.e., isolating the mixed noise. Mix data from different modalities and then try to reconstruct each using an encoder-decoder network.

14. Odd Segmentation Recognition: identify the unrelated subsegment that does not belong to the input under consideration.

15. Metric Learning with Triplet Loss: encourage the representations of similar inputs but different modalities to be closer, while the representations of dissimilar inputs to be further apart.

For time-series data with spatial variation, for example, multiple electrodes of EEG device placed around the surface of the head. Some pretext tasks are

1. Spatial rotation: the data is rotated in space.
2. Spatial shift: the data is shifted in space.
3. Sensor dropout: a random subset of sensors is replaced with zeros.
4. Sensor cutout: sensors in a small region of space are replaced with zeros.

Cheers! :smile:

##### References
* [Subject-Aware Contrastive Learning for Biosignals](https://arxiv.org/pdf/2007.04871v1.pdf)
* [Self-Supervised Representation Learning from Electroencephalography Signals](https://arxiv.org/pdf/1911.05419v1.pdf)
* [Sense and Learn: Self-Supervised for Omnipresent Sensors](https://arxiv.org/pdf/2009.13233.pdf)