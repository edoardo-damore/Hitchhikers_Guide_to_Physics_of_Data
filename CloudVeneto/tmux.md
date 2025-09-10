# Using `tmux` for Persistent Terminal Sessions
**tmux** (terminal multiplexer) is a powerful command-line tool that allows users to create, manage, and navigate between multiple terminal sessions from a single window. With tmux, you can split your terminal into panes, organize your work in tabs (called windows), and easily switch between tasks without opening multiple terminal instances. One of its most valuable features is session persistence: if your SSH connection drops or you log out, tmux keeps running in the background so you can reconnect and pick up right where you left off. It is especially useful when working on remote virtual machines, as it allows you to keep processes running even after closing the terminal. Here's how to use `tmux` effectively:

## The basics

### 1. Creating a New `tmux` Session
To start a new `tmux` session, use the following command:
```bash
tmux new -s <session_name>
```
Replace `<session_name>` with a name of your choice. This command creates a new session and attaches you to it.

### 2. Listing Existing `tmux` Sessions
If you have multiple `tmux` sessions running and want to see them, list the existing sessions with:
```bash
tmux ls
```
This command will display all active sessions, their names, and their IDs.

### 3. Attaching to an Existing `tmux` Session
To reattach to a `tmux` session that you've previously detached from, use:
```bash
tmux attach -t <session_name>
```
Replace `<session_name>` with the name of the session you want to reattach to. If you have only one session, you can simply use:
```bash
tmux attach
```

### 4. Detaching from a `tmux` Session
If you want to leave a `tmux` session running while closing the terminal or switching to another session, detach from it by pressing:
```
Ctrl + b, then d
```
This will leave the session running in the background.

### 5. Scrolling Through Terminal Output in a `tmux` Session
To scroll through the terminal output within a `tmux` session:
1. Enter copy mode by pressing:
   ```
   Ctrl + b, then [
   ```
2. Use the arrow keys or `PgUp`/`PgDn` to scroll through the output.
3. To exit copy mode, press:
   ```
   q
   ```

## Other commands

### 6. Splitting Panes

One of the most powerful features of `tmux` is splitting your window into multiple panes so you can run and monitor different processes side by side.

* Split vertically:

  ```
  Ctrl + b, then %
  ```
* Split horizontally:

  ```
  Ctrl + b, then "
  ```
* Switch between panes:

  ```
  Ctrl + b, then arrow key
  ```
* Close a pane:

  ```
  exit
  ```

### 7. Managing Windows (Tabs)

In addition to panes, `tmux` lets you create multiple windows within a session (like tabs in a terminal).

* Create a new window:

  ```
  Ctrl + b, then c
  ```
* Switch between windows:

  ```
  Ctrl + b, then n   # Next window  
  Ctrl + b, then p   # Previous window  
  Ctrl + b, then <number>  # Jump to a specific window
  ```
* List windows:

  ```
  Ctrl + b, then w
  ```

### 8. Renaming Sessions and Windows

For better organization, you can rename sessions and windows.

* Rename the current window:

  ```
  Ctrl + b, then ,
  ```
* Rename the current session:

  ```bash
  tmux rename-session -t <old_name> <new_name>
  ```

### 9. Killing Sessions

If you no longer need a session, you can kill it:

```bash
tmux kill-session -t <session_name>
```


### 10. Resizing Panes

You can resize panes if necessary:

```
Ctrl + b, then :resize-pane -L
Ctrl + b, then :resize-pane -R
Ctrl + b, then :resize-pane -U
Ctrl + b, then :resize-pane -D
```

(or hold `Ctrl + b`, then arrow keys if mouse mode is enabled).

---

### 11. Copy & Paste Text

You can copy and paste the text from the session. In copy mode:

1. Enter copy mode:

   ```
   Ctrl + b, then [
   ```
2. Start selection: press `Space`
3. Move to the end of the text, then press `Enter` to copy
4. Paste with:

   ```
   Ctrl + b, then ]
   ```

---

### 12. Session Navigation

Besides `tmux attach`, there are quick ways to move between running sessions directly from inside:

```
Ctrl + b, then s   # choose session from a list
```



### 13 (bonus). Customization

You can configure `tmux` to suit your workflow by editing the `~/.tmux.conf` file. Common tweaks include:

* Changing the prefix key (default `Ctrl + b`)
* Enabling mouse support for pane resizing and window switching
* Customizing colors and status bar

