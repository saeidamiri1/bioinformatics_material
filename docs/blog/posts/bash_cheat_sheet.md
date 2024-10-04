---
date: 2024-10-27
description: bash cheat sheet
categories:
  - linux  
---

# bash cheat sheet
Here are the bash scripts you frequently use to accomplish your tasks.

## User Information
### who
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

### whoami
It displays the system’s username:
```
whoami
```

### id
It displays the user identification, including the user ID and group ID:

```
id 
```

## System information
To display system and hardware information, you can use `uname` with various options.

|command|description|
|-|-|
`uname -a`|  print system information
`uname -s`|  kernel name
`uname -r`|  kernel release
`uname -m`|  system architecture
`uname -o`|  operation system


## File and directory commands
### pwd
This command displays the current working directory. We often use it with the `-P` flag, which shows the physical directory without any symbolic links:

```
pwd -P
```

### ls 
It displays a list of files and directories.
```
ls
```
ou can use it with the following flags:

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

### mkdir 
`mkdir` creates the directories
```
mkdir ./folder 
```
The `-p` flag can be used to create multiple directories at once.

```
mkdir -p ./folder/folder2/folder3 
```

### rm
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

### touch 
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

### cat
The `cat` command is used to create single or multiple files, view the contents of a file, concatenate files, and redirect output to the terminal or to files.

#### create file
By using the following command, you can create a file and add content. Once you’re done, press `Ctrl+D`.

```
cat > file1.txt
You care creating a file
```

#### View content
View the content 
```
cat  file1.txt file2.txt
```

#### Large file
If you have a large file that does not fit in the terminal, use `more` and  `less`

```
cat file.txt | more #show page by page
cat file.txt | less #show line by line
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

#### chown 
You can change the user and group.
```
chmod user:group file\folder
chmod -R user:group file\folder
```

With the `-R` flag, you can change the ownership of the directory and all its contents recursively.

#### chgrp
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

## Search 
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

## Search pattern in File
You can use `grep` command to search pattern in file. `grep pattern files`. The following  search for "hello" in the file.
```
grep "hello" file.txt 
```

If you want the command to be case-sensitive, use the `-i` flag.
```
grep -i "hello" file.txt
```

## ps
The `ps` command displays information about a selection of active processes.
```
ps
```

You can terminate active processes as follows:
```
kill <process_id>
```


## Curl Command
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


## History Command 
The `history` command displays a list of previously issued commands. There are a couple of options that can be used to modify the history.
```
history -c # clears the entire command history.
history -a # appends the current session's history to the history file.
```


## Useful references
-[ref]:  https://swcarpentry.github.io/shell-novice/
