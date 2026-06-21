# Panes
**Prefix:** `Ctrl + b`  
- **Vertical Split:** `Prefix` then `%`
- **Horizontal Split:** `Prefix` then `"`
- **Switch Panes:** `Prefix` then `Arrow Keys`
- **Close Pane:** Just type `exit` or hit `Ctrl + d`

# Sessions
List sessions.  
```shell
tmux ls
```

Start a session with name.  
```shell
tmux new -s <name>
```

Attach to a session.  
```shell
tmux attach -t <name>
```

Detach from a session.  
```shell
tmux detach -s <name>
```
Or: `Prefix` then `d`

Kill a session.  
```shell
tmux kill-session -t <name>
```
Or: `Prefix` then `:kill-session`

# Windows
Open a new window: `Prefix` then `c`.  
Switch to next window: `Prefix` then `n`.  
Switch to previous window: `Prefix` then `p`.

# Copy Mode
`Prefix` then `[`.