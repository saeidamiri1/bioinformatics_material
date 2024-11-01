---
date: 2024-10-27
authors:
  - saeidamiri1
description: cut
categories:
  - linux
authors:
  - saeidamiri1
---


# How drop specific columns
If you want to remove or keep specific columsn, you can `cut` command. 
<!-- more -->

Let  starts a new session and assigns it a name:
```
cat <<EOF > test.txt
c1 c2 c3 c4 
1 2 3 4
1 2 3 4
1 2 3 4
EOF
```

For an simple case, let use `cut` to just keep the columns 2 and drop the rest from the text file,  you can use `cut -d ' ' -f2 test.txt`, here  `-d ' '` specifies the field delimiter\space character instead of the tab character, which heresis . In the `-f` flag you can specifies the specific list of columns that are separated by . 
```
$ cut -d ' ' -f2 test.txt
c2
2
2
2
```
You can add more columns 
```
$ cut -d ' ' -f2,4 test.txt
c2 c4
2 4
2 4
2 4
```

```
$ cut -d ' ' -f 2-4 test.txt
c2 c3 c4
2 3 4
2 3 4
2 3 4
```


Now let revert that action and remove the second columns; use the previous command and add the `--complement` flag 

```
$ cut -d ' ' --complement -f2 test.txt
c1 c3 c4 
1 3 4
1 3 4
1 3 4
```

```
$ cut -d ' ' --complement -f2,4 test.txt
c1 c3 
1 3
1 3
1 3
```


You can use `-c`, to  selects only the characters specified. 
Below cut command prints characters after 3rd. 

```
$ cut -c  3-  test.txt
 c2 c3 c4 
2 3 4
2 3 4
2 3 4
```

Below cut command prints characters btween 3rd and 6th.   
```
cut -c  3-6  test.txt
 c2 
2 3 
2 3 
2 3 
```
