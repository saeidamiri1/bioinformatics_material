---
date: 2024-10-27
description: screen session
categories:
  - linux
authors:
  - saeidamiri1
---

# `screen` session
The `screen` session is a powerful command enables you to push running terminal applications to the background and bring them back to the foreground as needed. When using the `screen` command, processes can be detached from the session and reattached later. While the session is detached, the original process continues to run, managed by screen. When reattached, the session resumes with terminals intact, just as they were left. Additionally, screen supports split-screen displays and functions seamlessly over SSH connections, even after disconnection and reconnection.


<!-- more -->

Starts a new session and assigns it a name:
```
screen -S test
```

Displays the list of sessions.
```
screen -ls
```

Load the session 
```
screen -r <session_name> 
```

Forces detachment from another session.
```
screen -dr <session_name>
```

Quits the screen session from outside the session.
```
screen -XS <session-name> quit
```

Display the current session name: 
```
echo $STY
```

You can split window vertically 

```
Ctrl-a, Shift S # created vertical 
Ctrl-a, Tab # move to another window
Ctrl-a, c # create new session
Ctrl-a, Shift X # close the window. 
```

The following shows the shortcut and its action.

| shortcut | action |
|-|-|
|Ctrl-a Ctrl-d | Detach from the screen session|
|Ctrl-a c| Create a new window inside the screen session|
|Ctrl-a a |  Switch to the window that you were previously on|
|Ctrl-a " | List all open windows. Double-quotes " are typed with the Shift key|
|Ctrl-a Space| Switch to the next window|
|Ctrl-d | Exit out of the current window|
|Ctrl-a  Ctrl-esc| How to scroll up and down|

