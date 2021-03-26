---
title: "Adversarial Reprogramming and Adversarial Transferability"
date: 2020-01-02
mathjax: True
tags: [machine_learning]
categories:
  - machine learning
  - adversarial example
  - wearables
classes: wide 
---

Machine learning models have been shown to be vulnerable to adversarial examples for quite some time now. All the attack
methods that have been proposed uses some type of optimization trick to craft adversarial examples, such that the
adversary's goals of misclassification both targeted and non-targeted is achieved. These attack methods are designed with
the assumption that the adversary is only interested in the task for which the target model was trained for. For example, if
the target model is a MNIST digit classifier, then the adversary wants to either cause random misclassification that is 
classifying any digit image to number other than its original label. 

Now consider a case, where the adversary wants to use the MNIST classifier to classify image-net images. This will
require a new type of attack paradigm which will try to repurpose the already trained MNIST classifier into a image-net
classifier. This is exactly what *Adversarial Reprogramming* does. Adversarial reprogramming was introduced by Elsayed
et al., in their paper "*Adversarial Reprogramming Neural Networks*" as new class of adversarial attack. The authors
demonstrated how an adversary can repurpose a pre-trained image-net model for alternate classification tasks like MNIST
digits or CIFAR-10 images without modifying the network parameters.


**So what is Adversarial Reprogramming?**
To quote the authors from the paper, "*Adversarial reprogramming is a way to repurpose an existing neural network for a
new task chosen by the attacker, without the attacker needing to modify the network parameters.*"

**And how does it works?**

Consider classifier \\(f(x)\\) and an adversary who wishes to perform an adversarial task: for inputs \\(\bar{x}\\) (not necessarily in the same domain as \\(x\\)) the adversary wishes to compute a function \\(g(\bar{x})\\). 

The adversary can accomplish this by learning adversarial reprogramming functions \\(H_f(.;\theta)\\) and
\\(H_g(.;\theta)\\) that maps inputs and outputs between the two task. First the adversary converts the inputs
\\(\bar{x}\\) into \\(x\\) using the functions \\(H_f(.;\theta)\\) i.e., \\(H_f(\bar{x};\theta)\\) is a valid input to
the classifier \\(f\\). And the uses the function \\(H_g(.;\theta)\\) to maps the output of \\(f(H_f(\bar{x};\theta))\\)
back to the output of \\(g(\bar{x})\\). The parameters \\(\theta\\) of the adversarial program are then adjusted to
achieve \\(H_g(f(H_f(\bar{x};\theta))) = g(\bar{x}) \\). Here the \\(\theta\\) is called the adversarial program. 



