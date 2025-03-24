# keybinds

keybind config
```bash
bind <key> run-shell <command> # run command on keybind
bind -r <key> ... # repeat command on key
bind -n <key> ... # bind does not require prefix
```

commands
>[!hint]
>all tmux commands can be used in tmux using prefix + :
```bash
tmux # create new session
tmux a # attach to last session
tmux ls # list sessions
tmux kill-server # kill tmux
tmux neww # create new window
tmux split # create a vertical/horizontal split pane
tmux split -h # create a horizontal split pane
tmux display-message -a # dump env, can use in config using #<env>
tmux list-keys # view all keybinds, or bind ?
```

popup
```bash
# 75% term width, use current pane path, close when done
display-popup -E -d "#{pane_current_path}" -w 75%
```

st compat
```bash
# also set TERM=xterm-256colors or screen-256colors
export LC_CTYPE=en_US.UTF-8
```

# more cheat-sheets:

[tmux](https://tmuxcheatsheet.com/)
