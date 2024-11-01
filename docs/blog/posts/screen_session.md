---
date: 2024-10-27
description: screen session
categories:
  - linux
authors:
  - saeidamiri1
---

# `screen` session
One very useful command allows you to push running terminal applications to the background and bring them back to the foreground when needed. 
When a process is started with ‘screen’, the process can be detached from session & then can reattach the session at a later time. When the session is detached, the process that was originally started from the screen is still running and managed by the screen itself. The process can then re-attach the session at a later time, and the terminals are still there, the way it was left. It also supports split-screen displays and works over SSH connections, even after disconnecting and reconnecting!

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
|Ctrl-a d | Detach from the screen session|
|Ctrl-a c| Create a new window inside the screen session|
|Ctrl-a a |  Switch to the window that you were previously on|
|Ctrl-a " | List all open windows. Double-quotes " are typed with the Shift key|
|Ctrl-a Space| Switch to the next window|
|Ctrl-d | Exit out of the current window|
|Ctrl-a  Ctrl-esc| How to scroll up and down|

