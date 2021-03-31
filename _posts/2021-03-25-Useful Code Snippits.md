---
title: 	"Frequent and Useful Code Snippits"
date: 	2021-03-25
comments: True
mathjax: True
tags: [tools]
categories:
  - tools
  - utilities
---

A collection of useful and frequent code snippets that I am often trying to remember.

## Anaconda
### List Anaconda Environments
```bash
conda info --envs
```

### Update Anaconda
```bash
conda update -n base -c defaults conda
```

### Create a Conda Environment
```bash
conda create -n envName python=version
```

### Remove a Conda Environment
```bash
conda remove -n envName --all
```

### Remove all the downloaded tarballs for installed packages
```bash
conda clean --all    # no active envs needed
```

### Conda Revisions
Revisions allows us to track changes to our environment over time and roll-back to earlier time.

#### List revisions
```bash
conda list --revisions
```

#### Roll back to earlier time
```bash
conda install --revision revision_number
```

### Export Conda enviroment details
```bash
conda env export --file environment.yml
```

### Create a conda environment from environment YAML file
```bash
conda env create -n conda-env-name -f /path/to/environment.yml
```

### List installed packages in a conda environment
```bash
conda list
```


## Jekyll
### Run the Site Builder
```bash
bundle exec jekyll server --watch --livereload
```

## Jupyter
### Auto-import commonly used libraries
1. Create startup folder in ~/.ipython/profile_default
2. Create a python file start.py
3. Add imports in the file. 

```python
# start.py example
import numpy as np
import pandas as pd

# and so on ...
```


## Python
### Get memory usage of python script
```python
import os
import psutil
process = psutil.Process(os.getpid())
print(process.memory_info().rss)
```

### Set random seed for the project
```python
seed_value = 42
random.seed(seed_value)
np.random.seed(seed_value)
torch.manual_seed(seed_value)
torch.cuda.manual_seed_all(seed_value)
tf.random.set_seed(seed_value)
```


More code snippits can be found [here](https://amitness.com/cookbook/).