[Home](../README.md)

#### tmux
**Installation**  
```
$ sudo apt install tmux
```
**Create new sesion**    
For the first time, you can create a session with 
```
$ tmux new
```
Or, you can start a session with a session name
```
$ tmux new -sSessionName
```

**Basic commands**  
* `Ctrl+b c` Create a new window (with shell)
* `Ctrl+b w` Choose window from a list
* `Ctrl+b 0` Switch to window 0 (by number )
* `Ctrl+b ,` Rename the current window
* `Ctrl+b %` Split current pane horizontally into two panes
* `Ctrl+b "` Split current pane vertically into two panes
* `Ctrl+b o` Go to the next pane
* `Ctrl+b ;` Toggle between the current and previous pane
* `Ctrl+b x` Close the current pane

**Attaching and detaching**  
The attach-session command attaches to an existing session. Without arguments, 
it will attach to the most recently used session that is not already attached:
```
$ tmux attach
```
Or `-t` gives the name of a session to attach to:
```
$ tmux attach -tMySession
```
To detach tmux, the `Ctrl+b d` key binding is used
```
Ctrl+b d
```

**Listing sessions**  
The list-session command (`alias ls`) shows a list of available sessions that can 
be attached. This shows four sessions called 1, 2, myothersession and mysession:
```
$ tmux ls
1: 3 windows (created Sat Feb 22 11:44:51 2020)
2: 1 windows (created Sat Feb 22 11:44:51 2020)
myothersession: 2 windows (created Sat Feb 22 11:44:51 2020)
mysession: 1 windows (created Sat Feb 22 11:44:51 2020)
```

**Using the mouse**  
tmux has rich support for the mouse. It can be used to change the active pane 
or window, to resize panes, to copy text, or to choose items from menus.
```
$ tmux set -g mouse on  
```
Once the mouse is enabled:
* Pressing the left button on a pane will make that pane the active pane.
* Pressing the left button on a window name on the status line will make that 
  the current window.
* Dragging with the left button on a pane border resizes the pane.
* Dragging with the left button inside a pane selects text; the selected text 
  is copied when the mouse is released.
* Pressing the right button on a pane opens a menu with various commands. When 
  the mouse button is released, the selected command is run with the pane as 
  target. Each menu item also has a key shortcut shown in brackets.
* Pressing the right button on a window or on the session name on the status 
  line opens a similar menu for the window or session.

**Resizing and zooming panes**  
Panes may be resized in small steps with `Ctrl+b Ctrl+Left`, `Ctrl+b Ctrl+Right`,
`Ctrl+b Ctrl+Up` and `Ctrl+b Ctrl+Down` and in larger steps with `Ctrl+b Alt+Left`,
`Ctrl+b Alt+Right`, `Ctrl+b Alt+Up` and `Ctrl+b Alt+Down`. These use the resize-pane command.

A single pane may be temporarily made to take up the whole window with Ctrl+b Z
* any other panes are hidden. Pressing `Ctrl+b Z` again puts the pane and window
layout back to how it was. This is called zooming and unzooming. A window where
a pane has been zoomed is marked with a `Z` in the status line. Commands that 
change the size or position of panes in a window automatically unzoom the window.

**Killing tmux entirely**  
If there are no sessions, windows or panes inside tmux, the server will exit. 
It can also be entirely killed using the kill-server command. For example, 
at the command prompt:
```
$ tmux kill-server
```

#### References: 
* [tmux wiki](https://github.com/tmux/tmux/wiki/Getting-Started) 
* [Linuxize](https://linuxize.com/post/getting-started-with-tmux/) 
