---
title: 	"Installing Machine Learning Frameworks with Anaconda and Jupyter"
date: 	2020-02-01
mathjax: True
tags: 	[machine_learning, utilities]
---

# Installing Machine Learning Framework(s) with Anaconda and Jupyter 
Usually installing machine learning frameworks such as TensorFlow and PyTorch is bit of a hassle and setting up the
proper environment for development based on these frameworks becomes cumbersome than it should it. Although,
installation pages for TensorFlow and PyTorch are pretty good, they lack the details information one need to setup the
development environment easily with flexibility in mind. In this post, I am going to summarize the process I have used to setup the
development environment for machine learning project. I will try to include all the details I have found though trial
and error while installing these frameworks for myself. 

**1. Install Anaconda**

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
<img src="../assets/images/conda_init_bash.PNG" alt= "Initialize Anaconda for Git Bash."/>
</p>

**2. Setup the Virtual Environment**

The most important feature of Anaconda is that it allows us to create and manage multiple virtual environments. Using
virtual environments we can create development environment for different machine learning frameworks, without affecting
the base Python environment and other virtual environments. 

After a fresh installation of Anaconda, there will be just one environment i.e., the base. List the environments within
you anaconda distribution with the command:
```
conda info --envs
```
Execute this command in the Anaconda PowerShell or Git Bash. I will recommend the PowerShell because it will also show
you the current active environment. By default the base environment will be active.

<p align="center"> 
<img src="../assets/images/conda_env.PNG" alt= "List out the conda environments."/>
</p>

As you can see, I have 5 environments and I am currently in the base environment.

Say that you want to install the latest version of TensorFlow. To begin, first we will create a new virtual environment
named **testEnv**. Choose the name of the virtual environment based on your requirement, so that it has an informative
name for you. Here, I am creating this environment for demonstration purpose only. 
```
conda create -n testEnv python=3.7
```
Here, I am also specifying the Python version I want to use for this virtual environment.

<p align="center"> 
<img src="../assets/images/conda_create.PNG" alt= "Create a new virtual environment."/>
</p>

Press y, when prompted and the environment will be setup for you. Next, before doing anything we need to activate the
virtual environment you just created. 
```
conda activate testEnv
```
Notice that now you are in the activated virtual environment. 

<p align="center"> 
<img src="../assets/images/conda_activate.PNG" alt= "Activate the new virtual environment."/>
</p>

**3. Install the Machine Learning Framework(s) and other Libraries**
Next install the machine learning framework and libraries that you need. Since, we are using TensorFlow as an example,
I will install the TensorFlow and some other libraries. Install the TensorFlow using *pip*. You may need to upgrade the
*pip*. The install page on TensorFlow website will be useful here. Check it
[out](https://www.tensorflow.org/install/pip).
```
pip install --upgrade tensorflow
```

<p align="center"> 
<img src="../assets/images/conda_install_tf.PNG" alt= "Install TensorFlow."/>
</p>

Once the installation is done, you can install other libraries that you need using *pip*.



