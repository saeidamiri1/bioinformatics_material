---
date: 2024-10-27
description: Passwordless login linux system
categories:
  - ssh 
  - linux
  - password less
---

# passwordless ssh
We often use SSH (Secure Shell) to remotely connect to servers via the terminal. If you’re tired of entering a password every time you log in, follow the steps below to enable passwordless login.

## Add server info to config file
Open the SSH configuration file on your PC (the SSH client).
```
vim $HOME/.ssh/config
```

Add the server name, IP address (hostname), and the user ID for the server to the configuration file:
```
Host server1
HostName 8.8.8.8
User usr1
```

##  generate ssh key
Run the following command to generate new SSH keys:
```
ssh-keygen -t rsa
```

## copy key to server
Run the following command to copy the key to server1, and enter your password when prompted:
```
ssh-copy-id server1
```

You should now be able to log in to the server without entering a password.
```
ssh server1
```

Note: if you are using powershell in windows, use `cat ~/.ssh/id_rsa.pub | ssh usr1@HostName "mkdir ~/.ssh; cat >> ~/.ssh/authorized_keys"`

