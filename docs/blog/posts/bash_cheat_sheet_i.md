---
date: 2024-10-27
authors:
  - saeidamiri1
description: bash cheat sheet I 
categories:
  - linux
---

# Bash cheat sheet I 
Here are the bash scripts you frequently use to accomplish your tasks.

<!-- more -->

## User Information
### `who` command
It is used to retrieve information about the currently logged-in user on the system.
```
who
```

It provides the following information:
```
Login name of the user 
User terminal
Date & Time of login
Remote host name of the user
```

### `whoami` command
It displays the system’s username:
```
whoami
```

### `id` command 
It displays the user identification, including the user ID and group ID:

```
id 
```

## System information
To display system and hardware information, you can use `uname` command with various options.

|command|description|
|-|-|
`uname -a`|  print system information
`uname -s`|  kernel name
`uname -r`|  kernel release
`uname -m`|  system architecture
`uname -o`|  operation system


## File and directory commands

### `pwd` command
This command displays the current working directory. We often use it with the `-P` flag, which shows the physical directory without any symbolic links:

```
pwd -P
```

### `ls` command 
It displays a list of files and directories.
```
ls
```
or can use it with the following flags:

```
-a Show all files
-R list subdirectories recursively
-r Reverse order
-t Sort by last modified
-S Sort by file size, largest first
-l Use a long listing format
-1 One file per line
-m Comma-­sep­arated output
-Q Quoted output
```

The following command displays all files, including hidden ones.
```
ls -a 
```

### `mkdir` command 
`mkdir` creates the directories
```
mkdir ./folder 
```
The `-p` flag can be used to create multiple directories at once.

```
mkdir -p ./folder/folder2/folder3 
```

### `rm` command
It removes directories and files. To remove a file,
```
rm file.txt
```

To remove files forcefully without prompting for confirmation, use the `-f` flag.
```
rm -f file.txt
```

To remove a directory, use the `-r` flag.
```
rm -r folder
```

To move files or folders forcefully, use the `-rf` flag.
```
rm -rf folder
```

### `touch` command 
It can be used to create, change, and modify timestamps. The following commands create a file and multiple files, respectively:
```
touch file1.txt
touch file2.txt  file3.txt
```

Change only the modification time.
```
touch -m file2.txt
```

Change only the access time.
```
touch -a file2.txt
```

Use the timestamps of other files.
```
touch -r file1.txt file2.txt
```

### `cat` command
The `cat` command is used to create single or multiple files, view the contents of a file, concatenate files, and redirect output to the terminal or to files.

#### How create file
By using the following command, you can create a file and add content. Once you’re done, press `Ctrl+D`.

```
cat > file1.txt
You care creating a file
```
`>` is called  overwrite. 

#### How view content

View the content 
```
cat  file1.txt file2.txt
```

#### How view content of large file
If you have a large file that does not fit in the terminal, use `more` and  `less`

```
cat file.txt | more #show page by page
cat file.txt | less #show line by line
```

###  head and tail
You can use the `head` command to print the first few lines of its input. The following example shows how to print the first 10 lines.

```
head -10  file.txt 
```

The `tail` command is the opposite of head and prints the last few lines of its input.

```
head -10  file.txt 
```
### `wc` command
The `wc` command, which stands for 'word count,' has different flags: -l gives the number of lines, -w gives the number of words, and -m gives the number of characters. These flags can be combined to get all the information at once.

```
wc  -l  file.txt 
```

### `sort` command
The `sort` command will sort it's input. By default it will sort alphabetically but there are many options available to modify the sorting mechanism. The following code sorts the file based on the second column.

```
sort -t' ' -k2,2 file
```

The flags used are: <br>
<ul>
  <li><code>-t</code>: specifies the delimiter (in this case, a space). </li>
  <li><code>-k</code>: specifies the column for sorting. For example:
    <ul>
      <li><code>-k2</code>: means sorting based on the second column</li>
      <li><code>-k1,3</code>: means sorting from column 1 through column 3.</li>
      <li><code>-k1</code>: means sorting from column 1 through the end.</li>
    </ul>
  </li>
</ul>


### `echo` command
It can be used to display the text or message,
```
echo "First message"
```

It has `-e` flag that enable interpretation of backslash escapes. In the below, `\n` make new line. 

```
echo -e "First message \n Second message "
```
You store the result in the a file 

```
echo -e "First message \n Second message " > out.txt
cat out.txt
```

### Append vs overwrite  

We know `>` can be used to create a new file, and by reruning it create a new file. 

```
echo -e "First message \n Second message " > out.txt
cat out.txt
echo -e "First message \n Second message " > out.txt
cat out.txt
```

If you want to append, use `>>`

```
echo -e "First message \n Second message " > out.txt
cat out.txt
echo -e "First message \n Second message " >> out.txt
cat out.txt
```

## Variable 
Instead the file, you can store the value or message in a variable 
```
var1=Welcome
var2=20
```
To call them just dollar sign before the variable name 

```
echo $var1
echo $var2
```

You can call variable inside the `echo`
```
echo "$var1, I guess your age is $var2"
```

What we created are user variable, linux has many variables
```
echo $USER
```

here we had single wor, but if you assign comlex value, you need single quotes ( ' ) or double quotes ( " ). 

```
var3="Welcome to cheat sheet" 
echo $var3
```

You use `declare -i`  to set the type integer, 
```
declare -i var4=20
echo $var4

declare -i var5=Welcome
echo $var5
```

You define it as read only. 
```
declare -r var6="WEll"
var6="WEll2"
```
To cancel use `+`
```
declare +r var6="WEll"
var6="WEll2"
```

To determine the type of a variable
```
declare -p $var5
```




## bash Scripts
Instead of running a series of Bash commands interactively, we often place them in a file with a `.sh` file extension. Typically, we include `#!/bin/bash` at the top of the file, indicating that `/bin/bash` should be used as the interpreter to execute the script. If you place your script in the `~/bin directory`, it will be executable, provided `~/bin` is included in your `$PATH`. To check if `~/bin` is in your `$PATH`, run `echo $PATH`. If it is not included, you can add it to your `~/.bash_profile.`


```
PATH=$PATH:$HOME/bin
export PATH
```

`PATH` is an environment variable that contains a list of directories where executable programs are located. When you type a command in the command line, the system searches these directories, as defined by the PATH variable, to find the appropriate program interpreter. To make your script executable, run `chmod u+x file.sh` or `chmod 755 file.sh`.

```
> test.sh
#!/bin/bash
echo "WELCOME TO FIRST SHELL SCRIPT "
ls
echo "End of FIRST SHELL SCRIPT "

```
Then run 
```
bash test.sh
```

Users can modify the environment using the `set` command. By default, Bash does not handle errors automatically and leaves error handling up to the user. For example, the following commands will run without failing, even if an error occurs:

```
#!/bin/bash
echo $TEMP
echo Hello World
```

However, by adding `set -u`, Bash will treat the use of undefined variables as an error, causing the script to fail. For instance, if `$TEMP` is not defined, the script will exit with an error.

```
#!/bin/bash
set -u
echo $TEMP
echo Hello World
```

The following is a list of set options that can be used to control error handling in Bash:


| Set		|  Description |
|----| ----|
| `set -u`		| Exits script on undefined variables |
| `set -x`		| Shows command currently executing |
| `set -e`		| Exits script on error |
| `set -eo pipefail`	| Exits script on pipeline fail |

If you create a bash file, paset the following code in it and run it
If you create a Bash script, paste the following code into it, and run it
```
#!/bin/bash
myfunc | echo Hello World
echo Hi
```

you get the following
```
Hello World
aa.sh: line 2: myfunc: command not found
Hi
```

Now, add `set -eo pipefail` to observe the difference

```
#!/bin/bash
set -eo pipefail
myfunc | echo Hello World
echo Hi
```

```
aa.sh: line 3: myfunc: command not found
Hello World
```

### Comments
A comment in a script is a note meant for reference and clarity, and it is not executed. To add a comment, simply use a hash symbol (#); everything following it on the same line will be treated as a comment. Comments can occupy an entire line or be placed at the end of a line of code.

```
# First comment
echo "Welcome" # Second comment
```


### Command Subsitution
You can store the result of a command in a variable by placing the command within backquotes (`) and assigning it to the variable.

```
myvars=`ls /etc`
echo $myvars
```

You can also use `$()` to store the result of a command in a variable.

```
myvars=$(ls /etc)
echo $myvars
```

### Statue 
To check the result of the last executed command, use echo `$?`. If the output is 0, it means the command ran successfully.

```
> AAA
bash: AAA: command not found
> echo $?
127
> ls 
> echo $?
0 
```

It's important to note that even when an error is encountered, the script will continue running by default. To prevent this and stop execution on errors, use `set -e`.


### Global and Local Environment Variables
To view global environment variables, use the `env` command. To make environment variables persistent, add them to `~/.bashrc`. For example, to set a global variable `VAR="VALUE"`, open `.bashrc`  ( sudo nano ~/.bashrc) and add the line `export VAR="VALUE"`. To remove an environment variable, use the unset command. The following command deletes `MYVARIABLE`:


```
unset MYVARIABLE
``` 

## File permissions
You can define the access levels for files and folders to prevent people from accessing other users’ data without permission.

### Ownership
Each file\folder has three parts: <br />
u: user\owner of file who created it.  <br />
g: group of user who has access permissions of files\directories.  <br />
o: other users.


The following command shows the permissions of files and folders.
```
mkdir folder1
touch ./folder1/file.sh
touch ./folder1/file1.sh
ls -l ./folder1
ls -l file.sh
```

You can see it has four parts. <br />
1- first one digit: "-" or "d"<br />
2- second three digits: it shows the permission of owner. <br />
3- third three digits: designate permissions for the group. <br />
4- fourth three digits: designate permissions for the group. <br />


### Permissions
Each file or folder has three types of owners: <br />
- Read: It gives permission to open <br />
- Write: Permission to modify the contents of  files\folders.  <br />
- Execute: Give permission to run it.  <br />

The following shows the indicators of the permissions:
```
  r = read permission = 4
  w = write permission = 2
  x = execute permission = 1
  - = no permission = 0 
```

The following diagram shows the permissions.

<figure markdown="span">
  ![Image title](bash_cheat_sheet/diagram.png){ width="400" }
  <figcaption>Diagram</figcaption>
</figure>


|Symbol| Number | Permission Type | 
|-|-|-|
--- | 0 | No Permission
--x | 1| Execute
-w- | 2| Write	
-wx | 3| Execute + Write 
r-- | 4| Read	
r-x | 5| Read + Execute	
rw- | 6 | Read + Write
rwx | 7| Read + Write + Execute


### Change access
#### chmod 
It can be used to change the access mode. This command sets permissions (read, write, execute) on a file or directory for the owner, group, and others.

```
chmod [reference][operator][mode] file\folder
```
reference: u,g,o <br />
operator: The plus ("+") sign indicates give permission.  The minus ("-") sign indicates remove permission. <br />
mode: r,w,x <br />

**Examples** <br />
chmod a+r files:  readable by all  <br />
chmod a-r files: cancels the ability for all to read the file  <br />
chmod a-rwx cancels all access for all  <br />
chmod g+rw files give the group read and write permission  <br />
chmod u+rwx files give the owner all permissions <br />
chmod og+rw files give the world and the group read and write permission  <br />


The following command is a common command: <br />
chmod 755 file.txt:  <br />
Owner can read, write, execute files  <br />
Group can read and execute (use) but not change files. <br />
Other can read and execute (use) but not change.  <br />

#### `chown` command 
You can change the user and group.
```
chmod user:group file\folder
chmod -R user:group file\folder
```

With the `-R` flag, you can change the ownership of the directory and all its contents recursively.

#### `chgrp` command
It can be used to change the group owner. The `chgrp` and `chown` commands use the same system call and are functionally identical.

```
chgrp -R group file\folder
```

## Disk usage
You can use `du [option] [file/folder]` to check disk usage. The command `du ./folder` shows the disk usage summary of the `/folder` directory tree and each of its subdirectories.<br />
`du -h ./folder`:  to o determine the disk usage in a human-readable format.  <br />
`du -sh ./folder`: to find out the total disk usage.  <br />
`du  -ah /home/`: To determine the total disk usage of files and directories. <br />
`du  -ah --max-depth 2 /home/`: show total disk usage of all files and directories up to a certain depth. <br />
`du -ah --exclude="*.txt" /home/`: to find the total disk usage of files and directories while excluding files that match a given pattern.

## Networking
Display all network information. 
```
ipconfig -a 
```

Test the connection to a remote machine:
```
ping <ip-address> or hostname
```

Displays active or listening ports.
```
netstat -pnltu
```

## `find` command
You can use find to search for files and directories. The following command searches for `.txt` files:
```
find ./directory -type f -name '*.txt'
```
Search for empty files in the directory: 
```
find ./directory -type f -empty
```

Search for files with the specified permissions.
```
find ./directory -type f -perm 755
```

If you are looking for the path of command, use `whereis`,
```
whereis python3
```

## Wildcards
Wildcards are special characters used to create patterns that match sets of files or directories. Here are the common wildcards:

- `*`: Matches zero or more characters.
- `?`: Matches a single character.
- `[]`: Matches any character within the specified range.
- `!`: Excludes characters inside the brackets.
- `#`: Matches any single numeric character.


Let see some useful example. 

|example|descrition|
|---|---|
|d*|  any file that starts with the letter 'd'. |
|*.txt| any file with the .txt extension |
|??p*|  any file whose third letter is 'p'|
|*.???|  any file with a three letter extension|
| *# or *[0-9] |  any file that ends with a numeric character.|
|[bd]* | any file whose name either begins with  'b' or 'd'|
|*[0-9]* | any file whose name includes a digit in it |
|[a-d]* | any file whose name either begins with  'a', 'b', 'c', or 'd'|
|[!a-d]*  any file  which name does not start with 'a-d' |
|[[a-zA-Z0-9]]* | any file which name  starts alphanumeric character|

The following command will match any file with a name that contains an 'a' followed by zero or more characters, then a character that is not 'a', 'b', or 'c', and ending with the '.txt' extension.
```
ls a*[!abc].txt
```



## Search pattern in File
You can use `grep` command to search pattern in file. `grep pattern files`. The following  search for "hello" in the file.
```
grep "hello" file.txt 
```

If you want the command to be case-sensitive, use the `-i` flag.
```
grep -i "hello" file.txt
```

## `pwd` command
It stands for 'print working directory' and is used to display the current working directory.

## Process management
### `ps` command
The `ps` command displays information about a selection of active processes.
```
ps
```

You can terminate active processes as follows:
```
kill <process_id>
```


## `curl` Command
This command can be used to transfer data to or from a server. It supports various protocols, including HTTP, HTTPS, FTP, SFTP, etc. You can easily request an HTML page or a file.
```
curl -o aa.htlm  https://saeidamiri1.github.io/
```

Downloads a file and saves it with the same name as in the URL:
```
curl -O   https://saeidamiri1.github.io/
```

### Handling HTTP Requests
It allows you to send custom HTTP requests using various methods such as GET, POST, PUT, DELETE, etc. For instance, to send a GET request:
```
curl -X GET https://api.example.com/resource
```

Similarly, to send a POST request with data:
```
curl -X POST -d "key1=value1&key2=value2" https://api.example.com/resource
```

Includes custom headers in the request.
```
curl -H "Content-Type: application/json" http://example.com
```

### Uploading Files
In addition to downloading, you can also upload files using the `-T` flag. In the following example, the file is uploaded to the server.

```
curl -T uploadfile.txt ftp://example.com/upload/
```

### Authentication
By using the `-u` flag, you can specify the password.
```
curl -u username:password https://example.com/api
```

### Interrupted
If the download is interrupted for some reason, you can use the `-C -` flag:

```
curl -C - -O ftp://speedtest.tele2.net/1MB.zip
```


## `history` Command 
The `history` command displays a list of previously issued commands. There are a couple of options that can be used to modify the history.
```
history -c # clears the entire command history.
history -a # appends the current session's history to the history file.
```




## Useful references
-[ref]:  https://swcarpentry.github.io/shell-novice/
