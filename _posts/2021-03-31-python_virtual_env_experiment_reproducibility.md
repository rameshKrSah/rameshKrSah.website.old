---
title: "Code reproducibility and Python virtual environments."
date: 2021-03-30
comments: True
mathjax: True
tags: [python]
categories:
  - python
---

## Creating and managing Python virtual environments
<div style="text-align: justify">
In this article, we will learn to use Python's virtual environment to isolate our code while running it on the 
system and also adding reproducibility features.

A virtual environment is a Python tool for dependency management and project isolation. It allows us to run our code isolated 
from the system packages. We can create a virtual environment for each project with project specific packages and dependencies, 
allowing us to isolate our project from the system level packages and dependencies.

Lets assume that our project directory tree is
</div>

```bash
code/ 
--- hello.py
```

and the content of our ```hello.py``` is

```python
import os
import numpy as np

print(os.listdir())
```

<div style="text-align: justify">
As we can see I am importing numpy and printing all the directory in the root of this <code>hello.py</code> file. Now, let's create a Python virtual environment 
of name <code>myVirtualEnv</code> to run our <code>hello.py</code> script. 
</div>

```bash
python3 -m venv myVirtualEnv/
```

After this, the project directory tree will look like
```bash
code/ 
--- hello.py
--- myVirtualEnv/
```

<div style="text-align: justify">
The next step is to activate the virtual environment and install the numpy package since our <code>hello.py</code> needs to import numpy.
</div>

```bash
# activate the virtual environment
source myVirutalEnv/bin/activate
```

Now you should be in your virtual environment. Let's install the numpy. 
```bash
# install numpy 
pip install numpy
```

After this, we can run our ```hello.py``` script and see the output.
```bash
# run the hello.py script
puthon3 hello.py
```

Next to deactivate the virtual environment just run this command.
```bash
deactivate
```

## Reproducibility
<div style="text-align: justify">
When we share our code, we need to make sure that the person running our code has all the correct packages and dependencies setup. For this we can use 
the Python requirements file. The requirements file contains the name and version of all the packages needed to run the code. To generate the requirements 
file use the following command.
</div>

```bash
# do this with the virtual environment activated.
pip freeze > requirements.txt
```

<div style="text-align: justify">
Since we only installed the numpy package for our toy example the contents of the file will be 
</div>

```bash
# the numpy version number will be different
numpy==numpy_version_number
```

<div style="text-align: justify">
Now let's imagine your friend downloaded your code from Github and her project directory will lookslike this:
</div>

```bash
code/ 
--- hello.py
--- requirements.txt
```

<div style="text-align: justify">
Your friend will now create a virtual environment like we did before. After that she can install the required packages using the 
<code>requirements.txt</code> file like this.
</div>

```bash
# with the virtual environment activated
pip install -r requirements.txt
```

<div style="text-align: justify">
After this she can run the <code>hello.py</code> script without doing anything else. Isn't that neat :grin:
</div>

## Automating the whole process
<div style="text-align: justify">
Until now we have learned to create the virtual environment and install the required packagesn manually. How about automating this whole process with just one script file? 
We can create a script which creates the virtual environment, install the neccessary packages, runs the code, and finally remove or delete the virtual environment. For our example case, the script file <code> setup.sh </code> will look like this
</div>

```sh
#!bin/sh

# create the virtual environment named myvenv
python3 -m venv myvenv/

# activate the virtual environment
source myvenv/bin/activate

# install the necessary packages
pip install -r requirements.txt

# run the python script
python3 hello.py

# deactivate the virtual environment
deactivate

# delete the virtual environment
rm -r myvenv
```

To run the script do this
```bash
bash setup.sh
```

Here, I have assumed that you have Python 3 installed and your operating system is some variant of Linux. Similar can be acheived on MAC OS or Windows. 

Anaconda is a popular package manager for Python and other programming languages. In the next post, we will learn how we can achieve the process described 
above using Anaconda virtual environments. Cheers :grin:

