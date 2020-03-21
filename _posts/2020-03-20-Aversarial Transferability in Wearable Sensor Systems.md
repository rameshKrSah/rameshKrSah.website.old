---
title: 	"Adversarial Transferability in Wearable Sensor Systems"
date: 	2020-03-21
comments: false
mathjax: True
tags: 	[machine_learning, paper_article]
---

# Introduction
This article is brief summary of our paper on "[Adversarial Transferability in 
Wearable Sensor Systems](https://arxiv.org/pdf/2003.07982.pdf)." In this work we, 
have explored the topic of adversarial transferability from viewpoints that 
we believe are novel have not been discussed yet. But before we present our results 
and findings, let’s first understand a few topics and the framework of the paper.

# Adversarial Transferability
For the uninitiated, adversarial transferability captures the ability of adversarial 
examples that makes them transfer between independently trained models of different 
architectures. In almost all works on adversarial transferability, 
the discussion is usually carried out from the perspective of models. We believe 
in understanding adversarial transferability fully, and in uncovering the reasons 
behind their existence in the first place, we need to consider other avenues such 
as the datasets that are used to train the machine learning models. To this end 
in our work. We have tried to explore adversarial transferability and give a 
comprehensive discussion that takes into account the model and the dataset with 
wearable sensor systems as a case study.


# Discussion
In this work, we have explored adversarial transferability from the following perspectives. 
1. Transferability between machine learning models  
	In this case, we have trained models of different architectures independently on the 
same training set and evaluated them on adversarial examples computed using the 
deep neural network. The dataset we have used consists of features extracted from 
the time-series signals from different sensors for human activity recognition.
Figure 1 shows the training and test set accuracy of different classifiers. Here  
	- SVC: Support Vector Classifier
	- RFC: Random Forest Classifier
	- KNN: k-nearest neighbor Classifier
	- DTC: Decision Tree Classifier
	- LRC: Linear Regression Classifier
	- DNN: Deep Neural Network

<p align="center">
  <img src="../assets/images/transferability/clfs_acc.png" alt="Clfs Acc" style="width:80%"/>
  <figcaption align="center">Figure.1 - Classification accuracy of different classifiers on test and training set of the UCI feature dataset.</figcaption>
</p>

	Figures 2 and 3 show the misclassification rate and the success rate of untargeted and 
targeted (with target class sitting) adversarial examples computed using the DNN model 
for all the different classifiers. As we can confirm, the transferability of both 
untargeted and targeted adversarial examples are excellent in this scenario. Also   
	- FGSM: Fast Gradient Sign Method
	- BIM: Basic Iterative Method
	- MIM: Moment Iterative Method
	- SMM: Saliency Map Method
	- CW: Carlini Wagner  
	are the different attack methods we have used in our work. You can find more details about them in the paper.
	

<p align="center">
  <img src="../assets/images/transferability/ms_rate_untar_model_trans.png" alt="Model Untargeted Results" style="width:80%"/>
  <figcaption align="center">Figure.2 - Misclassification rate of different classifiers on untargeted adversarial examples computed using the DNN model.</figcaption>
</p>

<p align="center">
  <img src="../assets/images/transferability/acc_tar_model_trans.png" alt="Model Targeted Results" style="width:80%"/>
  <figcaption align="center">Figure.3 - Success rate of different classifiers on targeted adversarial examples computed using the DNN model.</figcaption>
</p>


2. Transferability Across Subjects  
	By subjects, we mean volunteers used in the study for data collection. 
For example, to collect sensor data for human activity recognition, 
labs recruit individuals to wear sensor systems on them. The collected sensor data 
is then used to train machine learning systems, which are then deployed in real-life 
cases in applications such as health monitoring, medicine adherence, etc. With 
transferability across subjects, we wanted to analyze how the different characteristics of individuals
used for data collection affect the transferability of adversarial examples.    

	We divided the MHEALTH dataset into two groups based on the subject ID: data from 
even ID subjects into one group and data from odd ID subjects into another. We then 
models on these dataset having same architectures and parameters. We computed untargeted 
and targeted adversarial examples using the even model (aptly named because it was trained on 
the data from even ID subjects :)) and evaluated these adversarial examples on both 
even and odd models. Figures 4 and 5 shows the performance of untargeted and targeted
adversarial examples on these models respectively.

<p align="center">
  <img src="../assets/images/transferability/mh_untar_ms_rate_cross_sub.png" alt="Model Untargeted Results" style="width:80%"/>
  <figcaption align="center">Figure.4 - Misclassification rate of even and odd models on the on untargeted adversarial examples computed using the even model.</figcaption>
</p>

<p align="center">
  <img src="../assets/images/transferability/mh_tar_acc_cross_sub.png" alt="Model Targeted Results" style="width:80%"/>
  <figcaption align="center">Figure.5 - Success rate of even and odd models on the on targeted adversarial examples computed using the even model.</figcaption>
</p>


# Conclusion