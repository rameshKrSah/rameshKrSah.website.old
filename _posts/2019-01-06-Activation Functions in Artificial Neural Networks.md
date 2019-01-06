---
title: 	"Activation Functions in Artificial Neural Networks"
date: 	2019-01-06
tags: 	[machine_learning]
---

In artificial neural networks, the activation function of a node defines the output of that node, or "neuron", given a 
set of inputs. This output is then used as input for the next node. A neural network without an activation function is 
essentially just a linear regression model. The activation function does the non-linear transformation to the input 
making it capable to learn and perform more complex tasks.
```python
Y = activation_function(sum(weight * input) + biases)
```
There are many types of activation functions and depending upon the appication we use the appropriate one.  

1. **Binary Step Function**
2. **Linear Function**  
3. **Sigmoid Function**  
4. **Hyperbolic Tan (Tanh) Function**
5. **Rectified Linear unit (ReLU) Function**
6. **Leaky Rectified Linear Unit (ReLU) Functioni**
7. **Softmax Function**

Depending upon the propertise of the problem we can make a better choice of activation function for easy and quicker 
convergence of the network.
- Sigmoid function and their combinations generally work better in the case of classifiers
- Sigmoid and tanh functions are sometimes avoided due to the vanishing gradient problem.
- ReLU function is a genral activation function ans is used in mose cases these days.
- If we encounter a case of dead neurons in our networks the leaky ReLU function is the best choice.
- Always keep in mind that ReLU function should only be used in hidden layers.
- As a rule of thumb, we can begin with using ReLU function and move over to other activation function in cases ReLU 
doesn't provide with optimum result.

### References  
[A nice atricle on the topic](https://www.analyticsvidhya.com/blog/2017/10/fundamentals-deep-learning-activation-functions-when-to-use-them/)  
[Wikipedia Article](https://en.wikipedia.org/wiki/Activation_function)
