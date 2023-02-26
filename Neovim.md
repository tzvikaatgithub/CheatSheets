NEOVIM
:neovim:nvim:lvim:

# Contents

- [References](#References)
- [Tips](#Tips)
- [Plugins](#Plugins)

# References

[Introduction | LunarVim Docs](https://www.lunarvim.org/#opinionated)

[GitHub - LunarVim/LunarVim: An IDE layer for Neovim with sane defaults. Completely free and community driven.](https://github.com/LunarVim/LunarVim)

[Editing in Lunar Vim is Magic — 8 Tips for Checking Out LVIM | by Nick McLean | Dev Genius](https://blog.devgenius.io/editing-in-lunar-vim-is-magic-8-tips-for-checking-out-lvim-69fd2083a47a)

[source code](ihttps://pragprog.com/titles/modvim/source_code)

[awesome neovim setup](https://github.com/Optixal/neovim-init.vim/blob/master/init.vim)

# Tips

Neovim uses two dirs to store configs and data (while Vim makes no such distinction)

`export VIMCONFIG=~/.vim`
`export VIMDATA=~/.vim`

`export VIMCONFIG=~/.config/nvim`
`export VIMDATA=~/.local/share/nvim`


to use neovim as the text editor for git commit
`export VISUAL=nvim`

create config dir for neovim
`mkdir -p ~/.config/nvim`

To run vim configs in neovim
`touch ~/.config/nvim/init.vim`

add to this file:

```
set runtimepath^=~/.vim runtimepath +=~/.vim/after
let &packpath = &runtimepath
source ~/.vim/vimrc
```

this would only not work with plugins that use job control, since the APIs are different

in neovim you can enable providers at runtime

`:checkhealth` runs diagnistic tests and details each provider

`py3 print('hello')`  runs a python3 script, for which you need a python client

neovim-remote

`python3 -m pip install --user --upgrade neovim-remote`

`nvr -h`

A package is a dir containing one or more plugins.

A plugin is a dir that contains one or more scripts.

A script contains instructions in vim script.

you can source the script `:source cone/myscript.vim` and then use commands from it `:mycommand`

basic structure:

```
demo-plugin
|
|--doc
|  |__demo.txt
|__plugin
   |__demo.vim
```

Installing a plugin means adding it to Vim's runtimepath

`:h runtimepath`

you can manually add an arbitrary path to runtimepath

`:set runtimepath+=$VIMCONFIG/arbitrary/demo-plugin`

or add plugins inside packages `$VIMCONFIG/pack/`, packages organize and load your plugins

better yet create `$VIMCONFIG/pack/bundle/` (here - `bundle` is a package) for plugins maintained by others and `$VIMCONFIG/pack/myplugins/` (here - `myplugins` is a package) for your own plugins

plugin that contains `/start/` will be loaded by the package which searches `/$VIMCONFIG/pack/*/start/` and loads whatever it finds into the runtimepath

after installing a plugin run `:helptags ALL`

Optional plugins are installed into `$VIMCONFIG/pack/bundle/opt/` which can be loaded with `:packadd vim-scriptease` where vim-scriptease is the plugin name. It will be available until nvim quits

`:scriptnames` shows which plugins are loaded

`:echo join(split(&runtimepath, ','), "\n")` shows your runtime paths, one per line

Manage plugins with minpac

install minpac as an optional plugin in `$VIMCONFIG/pack/minpac/opt` where minpac/ is the package name, inside `opt/` which makes it optional, install the plugin with `git clone`

Adding plugins with minpac is done by registering the plugin with `call minpac#add('github-username/plugin-name', {'type': 'opt'})` second arg is to make it optional, and it is optional :)

add `call minpac#add('k-takata/minpac', {'type': 'opt'})`

After registering, you need to update `:call minpac#update()` which installs new or updates existing plugins. To read messages launch `:messages` At which point you can restart nvim to start using them

To remove the plugin, first remove the line that adds it from .vimrc, then run `:call minpac#clean()`

`nvim +terminal` To start nvim with terminal right away

`:vsp | te` in cmd mode `|` is used to separate commands, when mapping in .nvimrc use `\|`

Scrolling

Command     Effect
`gg`          Jump to top of scrollback
`G`           Jump to bottom of scrollback
`<C-y>`       Scroll up one line
`<C-e>`       Scroll down one line
`<C-u>`       Scroll up half a page
`<C-d>`       Scroll down half a page
`<C-b>`       Scroll up a page
`<C-f>`       Scroll down a page

`gf` jupm to file path under coursor (and open it)

try this: ~/Documents/gcp.txt

Use this in the terminal buffer ;)

Open buffer in a split `:vert sb<nb>`

[Using Vim or NeoVim as a Git mergetool](https://www.grzegorowski.com/using-vim-or-neovim-nvim-as-a-git-mergetool)
# Plugins

[Vim/Neovim — Managing Databases. Managing databases and run SQL… | by alpha2phi | Medium](https://alpha2phi.medium.com/vim-neovim-managing-databases-d253faf4a0cd)
