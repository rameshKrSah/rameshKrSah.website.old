---
title: 	"Installing Machine Learning Frameworks with Anaconda and Jupyter"
date: 	2020-02-01
mathjax: True
tags: 	[machine_learning, utilities]
---

# Installing Machine Learning Framework(s) with Anaconda and Jupyter 
Unsually installing machine learning frameworks such as TensorFlow and PyTorch is bit of a hassle and setting up the
proper environment for development based on these frameworks becomes cumbersome than it should it. Although,
installation pages for TensorFlow and PyTorch are pretty good, they lack the details information one need to setup the
development environment easily with flexibility in mind. In this post, I am going to summarize the process I have used to setup the
development environment for machine learning project. I will try to include all the details I have found though trial
and error while installing these frameworks for myself. 

1. Install Anaconda 
First and foremost, we will need to install the [Anaconda](https://www.anaconda.com/distribution/) distribution package
manager. Anaconda will helps us setup the development environment very easily and provides a lot of flexibility in terms of creating and maintaining various virtual environment in our system without breaking any thing. 

Select the proper installer for your system and the Python version you need. I will suggest you to install the latest
Python version, since we can always create virtual environments for older Python version. The setup process is very
simple and similar to other programs. One extra thing with the setup process, is to add the Anaconda to system path.
Select the option for adding anaconda to the system path during the setup process. This will help us a lot later on. 

<p align="center"> 
<img src="../assets/images/conda_path.png" alt= "Add Anaconda to the System Path."/>
</p>


After installing the Anaconda manager, you need to activate it. To do this open the Anaconda PowerShell and execute the
command:
```
conda init
```

<p align="center"> 
<img src="../assets/images/conda_init.PNG" alt= "Initialize the Anaconda."/>
</p>


If you have Git Bash installed, then you can activate conda for Git Bash too so that you can use it from Git Bash. To
activate anaconda for git bash, open Git bash and execute the command:
```
conda init bash
```

<p align="center"> 
<img src="../assets/images/conda_init_bash.PNG" alt= "Initialze Anaconda for Git Bash."/>
</p>


