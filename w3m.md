# w3m
:w3m:

w3m is a cli browser that allows vim-like key bindings

`w3m <options> <url>`

[w3m short intro](https://www.howtogeek.com/103574/how-to-browse-from-the-linux-terminal-with-w3m/)

[w3m online manual](http://w3m.sourceforge.net/MANUAL)

Navigation - `h`, `j`, `k`, `l`

`<Tab>` move around

`<Enter>` select the input, or press a button/link

`U` - URL prompt (eg. <Ctrl>-L )
`u` - lookup the link address

`B` - back a page

`H` - help


# Tabs

`T` open new tab

`{` and `}` go back and forth between tabs

# Key Bindings

Default `ESC M` binding - browse link using external browser

The default `B` binding:
    - closes the buffer
    - goes out of the Help menu, (which is also a buffer?)

If you want just to move around, edit `~/.w3m/keymap` and add the following:

`keymap L NEXT`

`keymap H PREV`

To copy and paste cross platform, we define some keymaps to pbcopy, which in linux is an alias to xclip.
