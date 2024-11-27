---
date: 2024-10-27
authors:
  - saeidamiri1
description: How delete dubclicated lines
categories:
  - linux
  - awk
  - sort
authors:
  - saeidamiri1
---


# How remove duplicated lines 
## Using `awk`
Sometimes lines are duplicated in your text file. You can easily remove these duplicates using `awk`
<!-- more -->

```
awk '!seen[$0]++' files.txt
```

By adding the `-i inplace` flag, the original file is modified directly.

```
awk -i inplace  '!seen[$0]++' files.txt
```

To remove duplicate lines based on a specific column, such as the second column, replace `!seen[$0]++` to `!seen[$2]++`. 

```
awk -i inplace  '!seen[$2]++' files.txt
```

## Using `sort`
You can use sort to remove duplicates. The following code sorts the file and selects unique values based on the second column.

```
sort -u -t' ' -k2,2 file
```

The flags used are: <br>
<ul>
  <li><code>-u</code>: prints only unique lines. <br></li>
  <li><code>-t</code>: specifies the delimiter (in this case, a space). </li>
  <li><code>-k</code>: specifies the column for sorting. For example:
    <ul>
      <li><code>-k2</code>: means sorting based on the second column</li>
      <li><code>-k1,3</code>: means sorting from column 1 through column 3.</li>
      <li><code>-k1</code>: means sorting from column 1 through the end.</li>
    </ul>
  </li>
</ul>
