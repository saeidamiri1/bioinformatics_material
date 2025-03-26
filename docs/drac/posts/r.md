---
date: 2024-03-26
description: How to install your R module. 
categories:
  - Installing R library
authors:
  - saeidamiri1
---

# How 
To install your R module, refer to [DRAC](https://docs.alliancecan.ca/wiki/R), and follow the steps below:

<!-- more -->

## Load modules 
```
module load StdEnv/2023
module load r/4.4.0  
```

## Create your own path
Choose or create the appropriate path (choose a path that you have enough space) for installing the R library
```
mkdir -p /lustre03/project/6004655/COMMUN/runs/[Your ACCOUNT]/R/4.4
```

## Export path
```
export R_LIBS=/lustre03/project/6004655/COMMUN/runs/[Your ACCOUNT]/R/4.4
```

## Run 
```
R 
> .libPaths()
> # if it is no loaded, load from inside 
> R_LIB_PATH="/lustre03/project/6004655/COMMUN/runs/[Your ACCOUNT]/R/4.4";.libPaths(R_LIB_PATH) 
> # You can install it in 
> install.packages('sp', repos='https://cloud.r-project.org/', lib=R_LIB_PATH)
```
