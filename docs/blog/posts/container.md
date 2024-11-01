---
date: 2024-10-27
authors:
  - saeidamiri1
description: Container
categories:
  - linux
---

# Container 
A container is a lightweight package of an operating system that allows users to install software and its dependencies in isolated environments (called ‘containers’), making it a single, portable, shareable, and reproducible package, like Apptainer/Singularity or Docker. Unlike virtual machines, containers are lightweight, fast, and typically run on a Linux-based system. They are often best suited for running one or two applications.
<!-- more -->

## Apptainer/Singularity
Apptainer/Singularity is a free and open-source container framework designed to run scientific applications on HPC-backed resources or any operating system. Unlike Docker, Singularity allows non-privileged users to work with it, making it more suitable for HPC environments. In this guide, we introduce Apptainer/Singularity and demonstrate how to set up and use Singularity. We refer to it simply as Singularity, as it was formerly known, and many users still call it by that name.

`singularity` provides a command-line interface (CLI) to interact with containers. Run singularity --help to get an overview of Singularity and ensure it is installed correctly. You can also run the following command to test it.

```
$ singularity run library://godlovedc/funny/lolcow
 _______________________________________
/ Q: What's the difference between USL  \
| and the Titanic? A: The Titanic had a |
\ band.                                 /
 ---------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

## Downloading images
First, create the following folders:
```
mkdir -p  ~/test/data
mkdir -p  ~/test/singularity
```

Now download it into the provided folder.

```
cd ~/test/singularity
singularity pull docker://godlovedc/lolcow
ls 
```

## Enter
You can enter the container
```
$singularity shell lolcow_latest.sif
Singularity> 
```

Simply type an existing command in the container, e.g., `which cowsay`

```
Singularity> which cowsay
/usr/games/cowsay
```

This method allows you to execute commands within the container.

```
Singularity> cowsay 'I am within'

 __________
< I am within >
 ----------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

To exit, simply type `exit`:
```
Singularity> exit
exit
```

## Executing
To execute a containerized command from outside the container, use the `exec` command. This enables you to run commands within the container. For example:
```
$ singularity exec lolcow_latest.sif cowsay 'I am out'
 __________
< I am out >
 ----------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

## Redirection
You can redirect the output to your local system for further use.
```
singularity exec lolcow_latest.sif cowsay 'I am out' > cowsout
cat cowsout
```

## Pipes
You can also use pipeline techniques to execute commands with Singularity.
```
cat cowsout | singularity exec lolcow_latest.sif cowsay
```

## Building a Container
### Creating a container 
If you’re interested in creating your own container (called a sandbox), start with a Singularity definition file. This is a text file containing a series of instructions used to build a container image. Below is a simple definition file. In this example, we will install Python 3 and create the `/mydata` directory within the container.

```
cat <<EOF > ubuntu.def
Bootstrap: library
From: ubuntu:latest

%runscript
 echo "Container was created \$NOW"

%environment
    export LC_ALL=C

%labels
    AUTHOR saeid.amiri1@gmail.com
    Version v0.0.1

%post
    apt-get update && apt-get -y install python3 
    mkdir /mydata
EOF
```

The first two lines, `Bootstrap: library` and `From: ubuntu:latest`, specify that we want to pull the base image from the `library`, with the operating system being the latest version of Ubuntu. The rest of the file uses the `% prefix` to define different stages of the image build process. `%runscript`,  defines a script that will run when the container is started using the singularity run command. `%environment`,  defines environment variables for the container. `%labels` allows you to add metadata such as the author, version, etc. `%post` this section is where you can install software and pull files from remote locations. There are various options available to help you create an efficient container, see [documentaion](https://docs.sylabs.io/guides/3.5/user-guide/definition_files.html#sections). 

By running the following code, you can create your own container. Ensure you have `ubuntu.img` in the current directory. 

```
sudo singularity build --sandbox ubuntu.img ubuntu.def
```

### Modify containers
To modify your container, use `shell --writable` 
```
sudo singularity shell --writable ubuntu.img
```

Next, install the Nano text editor and write a simple Python script.
```
apt-get update
apt-get install nano
cd /opt
nano test.py
print("A simple code in Python")
```

### Test application
Run the following command to execute the Python script you created in the container.
```
$ singularity exec  ./ubuntu.img python3 /opt/test.py
A simple code in Python
```

### Accessing Host Files
Singularity has access only to files within the container. Therefore, if an application requires access to a specific file, you must mount it.

```
mkdir ./data1
echo 'Create first file' >   ./data1/test11.txt
echo 'Create second file ' > ./data1/test12.txt
```

Run the following command to check if the created folder is accessible within the container. By default, all folders stored in the container folder (on the host) are mounted inside the container.
```
$ singularity exec  ./ubuntu.img ls -l  ./data1
total 12
-rw-rw-r-- 1 sam sam 18 Oct  3 10:59 test11.txt
-rw-rw-r-- 1 sam sam 20 Oct  3 10:59 test12.txt
```

If a folder is not in the Singularity folder, you need to mount it using the `--bind (-B)` flag, which specifies the directories that must be linked between the host and the container.
```
mkdir ../data/data2
echo 'Create third file' > ../data/data2/test21.txt
singularity exec  --bind $HOME/test/data/data2 ./ubuntu.img ls -l $HOME/test/data/data2
total 4
-rw-rw-r-- 1 sam sam 18 Oct  3 11:23 test21.txt
```

You can bind mount a directory to a destination in the container using the source:destination syntax. By default, Singularity bind mounts several directories into your container, including `$HOME`, `/tmp`, `/proc`, and `/dev`. For example, to mount the directory `$HOME/test/data/data2` from the local system to `/mydata` within the container, use the following syntax:
```
singularity exec  --bind $HOME/test/data/data2:/mydata ./ubuntu.img ls -l /mydata 
```

You can bind multiple folders simultaneously.”
```
mkdir ../data/data3
echo 'Create fourth file' > ../data/data3/test31.txt

singularity exec  --bind $HOME/test/data/data2:/mydata,$HOME/test/data/data3:/tmp ./ubuntu.img ls -l  /mydata /tmp
```

You can use the environment variable `$SINGULARITY_BINDPATH`.
```
export SINGULARITY_BINDPATH=$HOME/test/data/data2:/mydata,$HOME/test/data/data3:/tmp
singularity exec  ./ubuntu.img ls -l  /mydata /tmp
```

### Sharing with other 
Once your container is ready, you can create a Singularity Image Format (SIF) file, which takes up less space, and share it with others.
```
sudo singularity build ./ubuntu.sif ./ubuntu.img
```

## Long-running Instances
If you want to run the container as a service for an extended period, which is particularly useful for operating as a web server or managing a database, use an instance to run it in the background.
```
singularity instance start lolcow_latest.sif cowsay 'I am within'
```

We can use the `instance list` command to show the currently running instances.
```
singularity instance list 
```

We can connect to running instances using the command `instance://<name_of_instance>`.
```
singularity shell instance://cowsay 
```

You can stop individual instances by using the command `instance stop <name_of_instance>`
```
singularity instance stop  cowsay 
```

## Image cache
Singularity does cache downloaded image files, which you can view using the singularity cache command:
```
singularity cache list
```

You can remove images from the cache by using the `singularity cache clean` command.

## Docker 
While Docker is widely used and has a large user community, it requires root privileges for many of its functions, which can pose security and compatibility challenges in high-performance computing (HPC) environments. Consequently, HPC systems often prefer alternatives that allow for secure, unprivileged containerization.

## Useful references
-[ref]:  https://hsf-training.github.io/hsf-training-singularity-webpage/
