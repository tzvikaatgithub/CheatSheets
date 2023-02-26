TMUX
:tmux:

Book: [Tao of Tmux](https://tao-of-tmux.readthedocs.io/en/latest/index.html)

Cheat Sheet: [Tmux Cheat Sheet](Tmux-Cheat-Sheet)

# Key Bindings
`<P>x` - kill current pane
`<P>w` - list windows
`<P>n` and `<P>p` - traverse windows
`<P>,` - name window
`<P>&` - kill window
`<P><space>` - toggle panes (layouts)
`<P>+` - break pane into window
`<P>-` - restore pane from window
`<P>{` and `<P>}` - move current pane counter and clockwise
`<P>t` - big clock
`<P>?` - list shortcuts

# Send Keys

`send-keys` command usees the same bindings as `bind-key`. Therefore you can use the [OpendBSD manual](https://man.openbsd.org/OpenBSD-current/man1/tmux.1#KEY_BINDINGS) to map what you send.

* `C-` or `^` ctrl
* `M-` alt
* `Up`
* `Down`
* `Left`
* `Right`
* `BSpace`
* `BTab`
* `Tab`
* `DC` (delete)
* `End`
* `Enter`
* `Escape`
* `F1`-`F12`
* and more

To bind '"' or "'" you need quotation around them.

`tmux send-keys -t right 'ls -l' C-m` send a command to the pane to the right

If sent from inside tmux, you don't use `tmux`, insted you do `<P>:`

# Window status symbols

`*` Denotes the current window.
`-` Marks the last window (previously selected).
`#` Window is monitored and activity has been detected.
`!` A bell has occurred in the window.
`~` The window has been silent for the monitor-silence interval.
`M` The window contains the marked pane.
    * Achieved by `<C-b>m`, this is called select-pane
`Z` The window's active pane is zoomed.
    * achieved by `<C-z>`

# Plugins Installed
    * [TPM](https://github.com/tmux-plugins/tpm) - plugin manager.
      Clone plugins into ~/.tmux/plugins
      `<prefix>I` - install plugins
      `<prefix>U` - updates plugins
    * [Online Plugins](https://github.com/tmux-plugins)
    * [Battery](https://github.com/tmux-plugins/tmux-battery)
    * [Tmux Solarized](https://github.com/seebi/tmux-colors-solarized/blob/master/README.md)
    * [Yank to Clipboard](https://github.com/tmux-plugins/tmux-yank) select and `<P>y`
    * [URL viewer](https://github.com/tmux-plugins/tmux-urlview) any URL in session. `<P>u`
    * [Direcotry Tree](://github.com/tmux-plugins/tmux-sidebar) `<P>e` - togle dir tree
      customize dir tree [link](https://github.com/tmux-plugins/tmux-sidebar/blob/master/docs/options.md)
# Plugins to Consider
    * [here](https://github.com/rothgar/awesome-tmux/blob/master/README.md)
# Tips
*Paste from a Buffer*
Everything you copy inside a session goes into consecutive buffers
To paste from a specific buffer, you can list them
`<C-prefix>=`
then simply select the one you want, it will paste it
you can also delete a buffer you don't need anymore from that screen
