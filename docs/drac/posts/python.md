---
date: 2024-03-26
description: How to install your Python module. 
categories:
  - Installing Python library
authors:
  - saeidamiri1
---

# How 
To install your Python module, refer to [DRAC](https://docs.alliancecan.ca/wiki/Python), and follow the steps below:

<!-- more -->

## Load modules 
```
module load StdEnv/2023
module load python/3.10  
```

## Create your own path
Choose or create the appropriate path (choose a path that you have enough space) for installing the R library
```
mkdir -p /lustre03/project/6004655/COMMUN/runs/[Your ACCOUNT]/Python/MYENV
```

## Create a virtual environment

```
virtualenv --no-download  /lustre03/project/6004655/COMMUN/runs/[Your ACCOUNT]/Python/MYENV
```

## Activate 
```
PYTHONENV0=/lustre03/project/6004655/COMMUN/runs/sanjath/MYENV
source $PYTHONENV0/bin/activate
export PYTHONPATH=$PYTHONENV0/lib/python3.10/site-packages
```

# Update pip
```
$PYTHONENV0/bin/python3.8 -m pip install --no-index --upgrade pip
```

# Install modules
By running the following code, the module will be installed in the virtual environment. 
```
$PYTHONENV0/bin/python3.8 -m pip install  matplotlib
```

## To run Python 
```
$PYTHONENV0/bin/python3.8
```

