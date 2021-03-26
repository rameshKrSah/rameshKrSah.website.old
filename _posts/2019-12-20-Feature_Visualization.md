---
title: "Feature Visualization of Human Activity Recognition Systems"
date: 2019-12-20
mathjax: True
tags: [machine_learning]
categories:
  - machine learning
  - har
classes: wide
---

For the class project of the Data Science course that I took during the fall 2019 semester at WSU, I choose to do a
project about feature visualization of machine learning models trained to do human activity recognition (HAR). The
motivation for me to choose this project was based on the fact that I was already working with HAR systems as part of my
research work and I always wanted to do some cool visualization of features learned by HAR systems. 

In this project my aim was to understand the working of human activity recognition systems. To this end I trained a CNN 
classifier on the raw sensor segment data and used class activation maps to show the importance of each value in
the input segment towards the decision made by the CNN classifier. In this blog post I will try to summarize the projects from all angles and showcase some results. But before we talk about the results I would like to give some background about human activity classification, convolutional neural networks and class activation maps.

# Human Activity Recognition (HAR)
The problem of human activity recognition can be defined as: Given a set \\(W = \{W_0,...,W_{m-1}\}\\) of \\(m\\) equally sized temporal window of sensor readings, such that each window \\(W_i\\) contains a set of sensor reading \\(S = \{S_{i, 0},...,S_{i, k-1}\}\\), and a set \\(A = \{a_0,...a_n-1\}\\) of \\(n\\) activity labels, the goal is to find a mapping function \\(f:S_i \to A\\) that can be evaluated for all possible values of \\(S_i\\). Raw data from various sensors, such as accelerometer, gyroscope, magnetometer, etc. are collected and passed into the signal processing stage, where filtering, noise removal, etc. are applied to the sensor signals. This is followed by a segmentation stage, where a continuous stream of a signal is divided into temporal windows. There are three types of segmentation: 1) activity-defined window, 2) event-defined window and 3) sliding window. In this project I have used the sliding window approach for dividing the sensor data into segments which were later used to train a CNN classifier.

# Convolutional Neural Network (CNN)
A convolutional neural network consists of an input and an output layer, as well as multiple hidden layers. The hidden layers of a CNN typically consist of a series of convolutional layers that convolve (multiply) the inputs with the filter. The convolutional layers parameters consist of a set of learnable filters or kernels, which have a small receptive filed, but extend through the full depth of the input volume. During the forward pass, each filter is convolved across the width and height of the input volume, computing the dot product between the entries of the filter and the input and producing a 2-dimensional (usually) activation map of that filter. As a result, the network learns filters that activate when it detects some specific type of feature at some spatial position in the input. The convolutional layers are usually followed by pooling layers such as max-pooling, min-pooling, and average-pooling. There can be regularization layers such as Dropout. Finally we will have a fully-connected layer that take the flattned matrix as input and give the prediction as the output.

<p align="center"> 
<img src="../assets/images/Typical_cnn.png" alt= "A convolutional neural network architecture."/>
</p>

# Class Activation Maps (CAM)
A class activation map for a particular category indicates the discriminative segments in the input sequence used by a
machine learning model to identify that category. It was first used to identify regions in an input image that
contributed the most towards the decision made by a image classifier. This image classifier was a CNN model with a
global average pooling layer. The importance of the image regions was identified by projecting back the weights of the
output layer on to the convolutional feature maps. This was possible because the global average pooling outputs the
spatial average of the feature map of each unit at the last convolutional layer. A weighted sum of these values is used
to generate the final output. Finally, the weighted sum of the features maps of the last convolutional layer is computed
to obtain the class activation maps.


For the training of the CNN classifier and getting the class activation maps I used the MHEALTH dataset which comprises body motion and vital signs recording for ten volunteers of diverse profile while performing 12 different physical activities. Sensors placed on the subject's chest, right writs and left ankle are used to measure the motion experienced by diverse body parts, namely acceleration, rate of turn and magnetic field orientation. All sensing modalities are recorded at a sampling rate of 50 Hz, which is considered sufficient for capturing human activity. Each session was recorded using a video camera for labelling the sensor reading accurately. The activities were performed in an out-of-lab environment with no constraint on the way these must be executed, with the exception that the subject should try their best when executing them.

For the experiments, I have selected the sensor data from the chest randomly and segmented the sensor reading into window segments using the moving window method. The window size is set to 2.56 seconds i.e., 128 samples in each window with a overlap of 50% between consecutive windows. In figure shown below we have the count plot showing the number of data samples for each class in the dataset. As you can see we have a total of 12 different activities classes but the class **Jump Front & Back** has very low number of samples compared to other classes. Hence, to balance the dataset I have removed the samples from the **Jump Front & Back** class before training machine learning models. 

<p align="center"> 
<img src="../assets/images/ds_project (7).png" alt= "Count plot for the MHEALTH dataset."/>
</p>

# Results
I used the TensorFlow package to train the CNN model. All the codes can be found on
[GitHub](https://github.com/rameshKrSah/ds_project_fall_2019). After training the CNN model for 46 epoch with early
stopping the classification accuracy on the training set was 93.88% and on the testing set was 93.99%. Figures below
shows the training curve with accuracy and loss on training and validation set and confusion matrix of the trained CNN
model on the test set.

<p align="center"> 
<img src="../assets/images/ds_project (8).png" alt= "Accuracy and loss on the training set and validation set for the CNN
model during training."/>
</p>

<p align="center"> 
<img src="../assets/images/ds_project (6).png" alt= "Confusion matrix of the CNN model on the test set."/>
</p>

From the confusion matrix we can see that the trained model is doing very well on most of the activities and is only struggling in between **Sitting** and **Standing** activities mostly. In the confusion matrix the vertical axis shows the true label and the horizontal axis shows the predicted label. As we can see the model is predicting 34 of the **Sitting** class samples as **Standing**. This again is completely justified by the nature of sensor data for these class. Since both of these class are stationary there is high probability that most of the data point in the sitting and standing class samples are very similar.

The next step was to plot the class activation maps on the sensor segments. To compute the class activation maps, we need the weights of the model and an input sample. The weight of the trained CNN is loaded into memory. By using the global average pooling layer just before the fully connected layer helps us to identify the complete extent of the segment within the input sample contributing to the decision of the model. This is because global average pooling takes an average across all the activation which helps to find all the discriminative regions. The spatial average of the feature map of each unit in the last convolutional layer is produced by the global average pooling layer which is then weighted summed to generate the final output. Finally, the dot product of the extracted weights from the final layer and the feature map is calculated to produce the class activation map. This class activation map is then upsampled and superimposed on the input sample to show the regions which the CNN model is looking at using a heatmap.

To produce the class activation maps we need input samples. To this end I randomly selected a sample from the following six classes: 1) Sitting, 2) Walking, 3) Climbing Stairs, 4) Running, 5) Knees Bending, and 6) Cycling. These selected classes I believe represents the dataset well based on their nature and differences. For example, since the sitting and the standing classes are very similar to each other, it doesn't make sense to include these two simultaneously. The figures below shows the activation maps for the selected samples. 

<p align="center"> 
<img src="../assets/images/ds_project (4).png" alt= "Activation map for a sample from the Sitting class."/>
</p>

For the *sitting* class, we can see that data points corresponding to the small movements are weighted more than the rapid changes in the sensor signal. This makes sense because while sitting, any person is not moving very much but also is not completely still.

<p align="center"> 
<img src="../assets/images/ds_project (5).png" alt= "Activation map for a sample from the Walking class."/>
</p>

For the *walking* class we see the opposite pattern to that of the *sitting* class. Here the rapid changes in the sensor signal is weighted more than the slow changes. This again is because while walking an individual experience a wider range of variation.


<p align="center"> 
<img src="../assets/images/ds_project (9).png" alt= "Activation map for a sample from the Climbing Stairs class."/>
</p>

Judging by just our intuition we will guess that the activation map for the *Walking* class and the *Climbing Stairs* class will be very similar, because of the similarity between these two activities. But from the activation map shown above, we can see that two classes have some significant differences. For the *Climbing Stairs* class, the data points which have very significant differences between them are weighted the most where as most of other data points are assigned very low weight. Hence, the CNN model is looking for these significant change in the value of the data points when deciding for the *Climbing Stairs* class.

<p align="center"> 
<img src="../assets/images/ds_project (3).png" alt= "Activation map for a sample from the Running class."/>
</p>

For the *Running* class, most higher value data points are assigned greater weight as evident in the above figure. So
any rapid changes in the sensor value is the driving characteristics that the CNN model is looking for when deciding
on the *Running* class. 

<p align="center"> 
<img src="../assets/images/ds_project (2).png" alt= "Activation map for a sample from the Knees Bending class."/>
</p>

<p align="center"> 
<img src="../assets/images/ds_project (1).png" alt= "Activation map for a sample from the Cycling class."/>
</p>

# Conclusion
In this project we tried to understand the working of human activity recognition systems. To this end I trained a CNN classifier on the raw sensor segment data and used class activation maps to show the importance of each value in the input segment towards the decision made by the CNN classifier. I selected six different activities 1) Sitting, 2) Walking, 3) Climbing Stairs, 4) Running, 5) Knees Bending, and 6) Cycling for visualization. A random sample for each activity was obtained from the test set, and the class activation map for each sample was computed and plotted. From these graphs we can see that how the different signal characteristics affects the decision of the CNN classifier. We have shown that for activity involving higher degree of motions like running and cycling, rapid changes in the sensor signal has more weight to the decision made by the CNN model. And similarly for activities with lesser motions like sitting and knees bending slower changes and trend in the signal contributes more towards the decision made by the CNN model. From the these experiments we have tried to understand the inner working of a human activity recognition system and I believe the findings shown in this paper certainly helps us interpret the deep neural network models and answer fundamental questions like "Why do these deep model work so well?" and "What are these deep network basing their decisions on?".


