

# https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533

```bash
# creates the conda environment in the default environment folder
conda create --name conda_env_name python

# create a conda environment in user specified folder
conda create --prefix /path/to/conda_env
```

```bash
# activates the conda environment in the default environment folder
conda activate conda_env_name

# activate the conda environment in the user specified folder
conda activate /path/to/conda_env
```

```bash
conda install numpy
```

```bash
python3 hello.py
```

```bash
conda deactivate
```

```bash
conda env export > enviroment.yml
```

```bash
conda env create -n conda_env -f /path/to/environment.yml
```

```sh
#!bin/sh

conda env create -n --prefix /path/to/conda_env/ -f /path/to/environment.yml
conda activate /conda_env
python3 hello.py
conda deactivate
conda remove -n --prefix /path/to/conda_env --all
```
