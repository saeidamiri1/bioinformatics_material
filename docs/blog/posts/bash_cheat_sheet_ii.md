---
date: 2024-10-27
authors:
  - saeidamiri1
description: bash cheat sheet II 
categories:
  - linux
---

# Bash cheat sheet II  
Here we present the continuation of [Bash cheat sheet I](./bash_cheat_sheet_i.md), providing more advanced Bash commands.

<!-- more -->

## Bash Configuration
Linux includes several configuration files that can be used to manage the system. To view the existing Bash configuration files, run the following command.

```
ls -a ~/ | grep bash
```

### `.bashrc`
The `.bashrc` file is a configuration file (shell script) that runs whenever a shell session is started interactively. When you open a command shell, this file is executed. The purpose of the `.bashrc` file is to up environment variables, functions, aliases, customize the prompt, and configure other settings that should be applied each time a new terminal window is opened. If you modify the `.bashrc` file, you can refresh the current shell session without closing the terminal by running `source ~/.bashrc`.


### `.bash_profile`
The `.bash_profile` is executed when you log in interactively through the terminal, while .bashrc is executed for interactive non-login shells. If you make changes to these files, they won't take effect until the next login session. Typically, `~/.bash_profile` includes commands to source the `.bashrc` file. This ensures that both files are read and executed each time you log in to the terminal.

```
if [[ -f ~/.bashrc ]]; then
	. ~/.bashrc
fi
```
Note, most Linux distributions are using `~/.profile` instead of `~/.bash_profile`. The `~/.profile` file is read by all shells, while `~/.bash_profile` only by Bash.

### `.bash_history`
By default, Bash saves the command history in the `~/.bash_history` file. The history command typically shows commands from the current terminal session. However, the commands saved to `~/.bash_history` are those from the last session when you log out.


## Redirecting and piping
The output of any command can be either standard output (stdout) or standard error (stderr), and both can be redirected or discarded as needed. 

## Redirecting to a file 
Using the classic redirection operator (command > file), stdout is redirected to the specified file, while stderr is displayed in the terminal. To redirect stdout to out.log and stderr to err.log, you can use the following commands:

```
command > out.log 2> err.log
```

To discard output, redirect it to `/dev/null`, which acts as a null device where anything sent to it is not stored. For example, to log stdout while hiding errors, use:

```
command  > out.log 2> /dev/null
```

To send both stdout and stderr to out.log, use the following command:
```
command> out.log 2>&1 
```

Alternatively, you can use:
```
command  &> out.log  
```

so you get no output
```
myprogram &>/dev/null 
```

So, using either of these methods, you will get no output in the terminal because both stdout and stderr are redirected to the out.log file

```
ls -l /bin 2> /dev/null
ls -l /bin/TEST 2> /dev/null
```

### Redirecting from a File
To redirect input from a file, you can use (command < file), which sends the contents of a file as input to a command. For example, to understand this, consider the command `wc -l`:
```
wc -l file.txt
10 file.txt
```
You can redirect a file as input to wc -l by using the < symbol:

```
wc -l < file.txt
10 
```
If you want to redirect input to a command and then redirect the result to a file instead of displaying it in the terminal, you can use the following code.

```
wc -l < file.txt > result.out
```

### Piping
To send the output of one command as input to another, we use piping, which has a simple structure: the `|` symbol is placed between commands. For example, let's run `ls`.
```
ls 

README.md               docs                    package.json
TODO                    material                pyproject.toml
codes                   mkdocs.yml              site
debug.log               package-lock.json       test.txt

```

To send the output of one command to another and shorten the result, we use piping with the `|` symbol between commands
```
ls | head -4
README.md
TODO
codes
debug.log
```
We can use multiple instances of piping to send the output of one command to another command and continue chaining them as needed. The `|` symbol is used between commands for this purpose.
```
ls | head -4 | tail -2  
codes
debug.log
```

We can take this further by redirecting the output to a file or another location using the `>` symbol.
```
ls | head -4 | tail -2  > pipe.out
```

## Arrays
You can store multiple values in a single variable, referred to as an array. The structure is simple: enclose the values in parentheses and separate them with spaces. Array indexing starts from 1.

```
myarray=("first" "second" "third")
echo $myarray
echo ${myarray[1]}
echo ${myarray[2]}
```

## Conditional
The conditional structure in Bash follows a standard format. The general structure is called an `if-elif-else` statement, which evaluates a series of conditions that may lead to different paths of execution

```
if <condition1>; then
    <commands>
elif <condition2>; then
    <other_commands>
else
    <fallback_commands>
fi
```


It can also be rewritten as an `if-elif` statement or an `if-else` statement. In some cases, we want to execute one of actions if a condition is true, and another if it is false.

```
if <condition1>; then
    <commands>
elif <condition2>; then
    <other_commands>
fi
```

```
if <condition1>; then
    <commands>
else
    <fallback_commands>
fi
```

Each conditional statement evaluates a single condition (which can be a combination of multiple conditions) and performs an action (or a series of actions). Let's look at the following example, which tests the number of files in the current directory.

```
VAR=`ls -1 | wc -l` 
echo "Testing the number of files"
echo "======================"
echo ""


if [[ $VAR -eq 2 ]] then
        echo " number of file is 2"
else 
     echo "number of file is not 2"
fi
```

You can replace the `-eq` (numeric comparison) operator with the `==` (string comparison) operator in some cases.

### Number evaluation
The following table includes comparison operators that can be used to compare numbers:

| Expression | escription | symbol Operators | 
|-----|-----|-----|   
| value1 -eg value 2 |  tests if two values/variables are equal | = or ==| 
| value1 -ne value 2 |  checks if two values/variables are not equal | != |
| value1 -le value 2 |  checks if one value is equal or less than another |  <= |
| value1 -lt value 2 |  checks if one value is less than another | <| 
| value1 -ge value 2 |  checks if one value is greater than or equal to another | >= |
| value1 -gt value 2 |  checks if one value is greater than anothe |  <  |


### String evaluation
The following table includes comparison operators that can be used to compare numbers:

| Expression | escription |
|-----|-----|
|-n string| returns true if the length of string is greater than zero|
|-z string| returns true if The length of string is zero|
| string1 == string2| The string1 and the string2 are equal|
| string1 != string2| The string1 and the string2 are not equal|
| string1 < string2| The string1 sorts (ASCII) before the string2|
| string1 > string2| The string1 sorts (ASCII) after the string2|


### File Evaluating 
Let's create a test file and check if we can test its existence using a conditional statement.
```
echo "ABC" > test.txt
FILENAME=test.txt1
echo "Testing for the existence of a file called $FILENAME"

if [[ ! -a $FILENAME ]]
    then
        echo " $FILENAME does exist "
fi

# negation operator 
if [[ ! -a $FILENAME ]]
    then
        echo " $FILENAME does not  exist "
fi
```

The following table presents the operators that allow you to assess and compare files in Bash.

| Expression | Description |
|-----|-----|
| file1 -nt file2 | compares the creation dates of two files to see if one file (file 1) is newer than the other (file 2) |
| file1 -ot file2 | compares the creation dates of two files to verify if one file (file 1) is older than the other (file 2) |
| file1 -ef file2 | checks if two variables are hard links to the same file |
| -e | validates the existence of a file (returns true if a file exists) |
| -f | validates if the variable is a regular file (not a folder, directory, or device) |
| -d | checks if the variable is a directory |
| -h (or -L) | validates if the variable is a file that is a symbolic link |
| -b | checks if a variable is a block special file |
| -c | verifies if a variable is a character special file |
| -p | checks if a file is a pipe |
| -S | checks if a file is a socket |
| -s | verifies if the size of the file is above zero (returns true if the file is greater than 0 bytes) |
| -t | validates if the file is associated with a terminal device |
| -r | checks if the file has read permissions |
| -w | verifies if the file has write permissions |
| -x | checks if the file has execute permissions |
| -g | checks if the SGID flag is on a file |
| -u | verifies if the SUID flag is on a file |
| -k | checks if the sticky bit is on a file |
| -O | verifies if you’re the owner of a file |
| -G | validates if the group ID is the same as yours |
| -N | validates if a file was modified since it was last read |


## Case Statements
Case statements can be very useful when you want to control the flow of execution based on different conditions. 
```
case <test variable> in
<test pattern1>)  <perform task>;;
<test pattern2>) <perform task>;;
<test pattern3>) <perform task>;;
……………
esac
```

```
n=`ls -1 | wc -l` 
echo $n

case $n in 
0) echo "There are no files here \n";; 
1) echo "There is one \n";;
2) echo  "There are two files here \n";; 
3) echo  "There are three files here \n";; 
4) echo  "There are four files here \n";; 
*) echo "There are more than four files here \n";; 
esac
```

The pattern `*` acts as a catch-all and will match if none of the other patterns match.

```
n=`ls -1 | wc -l` 
echo $n

case $n in 
0|2|4) echo "There are even number of files here \n";; 
1|3|) echo "There are odd number of files here \n";;
*) echo "There are more than four files here \n";; 
esac
```




### Control operator
You can combine multiple conditions using `&&` (and) and `||` (or) to create alternative logical expressions:

- `&&` means execute the statement that follows only if the preceding statement is successful (i.e., it returns an exit code of zero). For example, `command1 && command2` will only run command2 if command1 is successful.

- `||` means execute the statement that follows only if the preceding statement fails (i.e., it returns a non-zero exit code). For example, `command1 || command2` will only run command2 if command1 fails.


```
VAR=`ls -1 | wc -l` 
echo "Testing the number of files"
echo "======================"
echo ""


if [ $VAR -eq 2 ] ||  [ $VAR -eq 3 ] then
        echo "number of file is 2 or 3"
else 
  echo "number of file is not 2 or 3"
fi
```

The `if-else` statement can be simplified using `||` and `&&`. For example, you can replace an `if-else` structure with these logical operators to handle success and failure conditions in a more compact form.

```
if <condition1>; then
    <commands>
else
    <fallback_commands>
fi
```

```
<condition1> && <commands> || <fallback_commands>
```

Other control operators include:

- `&` means execute the preceding statement in the background.
- `;` execute the preceding statement and, once it completes, proceed to the next statement.
- `|` or piping: executes the preceding statement and connects its stdout to the stdin of the following statement.


## Loops in Bash 
Bash supports different types of loops to repeatedly execute a of commands. By using conditional statements, you can have complex control over the flow of the code.

### For Loop
For loops in Bash are used to iterate over a list of items. The general syntax of a `for` loop is as follows:

```
for <VAR> in <list of item>; do
    <command>
done
```

The list of items can be a space-separated list of values or the output of a command that returns a list of items

```
for i in 1 2 3; do
   echo "Welcome $i times"
done
```

You can define a range of numbers or characters using the sequence expression. For a range of numbers, we often use `{START..END..STEP}`. For example, `{1..10..2}` generates 1 3 5 7 9.

```
for i in {1..10..2}; do
   echo "Welcome $i times"
done
```

You can also use an array to define a list of items:

```
myarray=(aa bb cc)
for i in $myarray; do
   echo "Welcome $i times"
done
```


### While Loop
The `while` loop is used to execute commands as long as a condition is true. The general syntax for a `while` loop is as follows:

```
while  <conditions>; do
    <command>
done
```

The following runs a list of commands repeatedly as long as a specified condition is true:

```
COUNT=1
NUM=10
while [[ $COUNT -le $NUM ]]
do
    echo "repear number $COUNT"
    COUNT="`expr $COUNT + 1`"
done
```

It can be simplified as follows:

```
COUNT=1
NUM=10
while [[ $COUNT <= $NUM ]]
do
    echo "repear number $COUNT"
    ((COUNT++))
done
```

### `break` and `continue` Statements
You can use the `break` and `continue` statements to implement complex conditions within loops and control the flow of the code. In the following example, we use break to exit the `for` loop.

```
for i in {1..10..1}; do
   echo "Welcome $i times"
   if [ $i -eq 5 ]
   then
       break
   fi 
done
```

Let's look at the following example: when the counter is greater than 6, it skips the rest of the loop.

```
for i in {1..10..1}; do
   if [ $i -ge 6 ]
   then
       continue
   fi
   echo "Welcome $i times" 
done
```

## Error Handling
In the [#statue](./bash_cheat_sheet_ii.md/#statue), we see how to use `$?` to check the status of the last command., 


```
DIRECTORY=./TEMP
cd $DIRECTORY

if [ $? -eq "0" ]; then
    echo "Last command was run successfully"
else
    echo "Last command was not run successfully"
fi
```

## Functions
The structure of a function in Bash is as follows:

```
function name () {
   <command>
}
```

```
funcexample () {
    VAR=`ls -1 | wc -l` 
    echo "Run from inside"
    echo $VAR
}

funcexample
```

You can pass arguments to a function in Bash. `$1` represents the first argument, `$2` the second, and so on. Other special variables include `$0` (the name of the function), `$*` (all arguments), and `$#` (the number of arguments).

```
funcexample () {
  echo "First parametr $1"
  echo "Second parametr $2"  
  echo "Name of function is $0"
  echo  "All of arguments $*"
  echo "Number of arguments $#"
}
funcexample Welcome 10 
```

You can use the `return` statement to return a value from a function in Bash.

```
funcexample () {
    if [[ $# > 1 ]]; then
        echo "You have  $# params"
        return $#
    else
        echo "No params"
        return NA
    fi
}

funcexample Welcome 10 
```