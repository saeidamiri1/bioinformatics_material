---
date: 2024-10-27
authors:
  - saeidamiri1
description: How remove the dupclicated columns
categories:
  - linux
  - awk
authors:
  - saeidamiri1
---


# How remove the dupclicated columns
## Using `awk`
Sometimes columns are duplicated in your text file. You can easily remove these duplicates using `awk`
<!-- more -->

```
awk 'NR==1{for(i=1;i<=NF;i++)b[$i]++&&a[i]}{for(i in a)$i="";gsub(" +"," ")}1' 
```
