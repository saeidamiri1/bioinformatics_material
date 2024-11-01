---
date: 2024-10-27
authors:
  - saeidamiri1
description: tr
categories:
  - linux
---

# `tr` command
The `tr` command is very useful command in deleteing or replaceing character

<!-- more -->

## Replace Newline with Comma
Let  starts a new session and assigns it a name:
```
cat <<EOF > test.txt
c1 c2 c3 c4 
1 2 3 4
1 2 3 4
1 2 3 4
EOF
```

Run `cat test.txt | tr -s '\n' ','`,  the `-s` flag determina what you wan to replace, here we interestted in new line `\n` 

```
% cat test.txt | tr -s '\n' ','
c1 c2 c3 c4 ,1 2 3 4,1 2 3 4,1 2 3 4,%    
```


## drop repeated spaces
We use `tr -s ' '` to convert any repeated spaces into a single space: 
```
cat <<EOF > test2.txt
c1 c2 c3    c4 
1 2 3 4
1 2 3 4
1 2 3 4
EOF
```
cat test.txt | tr -s ' '
```
$ cat   test2.txt
c1 c2 c3    c4 
1 2 3 4
1 2 3 4
1 2 3 4
$ cat test.txt | tr -s ' '
c1 c2 c3 c4 
1 2 3 4
1 2 3 4
1 2 3 4
samamiri@beluga1:~$ 
```




## specified characters 
```
$ cat test.txt | tr  "c1" "C5"
C5 C2 C3 C4 
5 2 3 4
5 2 3 4
5 2 3 4
```

Let drop the digitals from file 
```
 cat test.txt | tr -d [:digit:]
c c c c 
   
   
   

```

Or invertly keep the digital 
```
 cat test.txt | tr -cd [:digit:]
 1234123412341234
```


To convert characters from lower case to upper case, you can either specify a range of characters or use the predefined character classes. 

```
echo "hello" | tr [:lower:] [:upper:]
HELLO
echo "Hello" | tr [:upper:] [:lower:] 
hello
```