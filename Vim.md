VIM
:vim:

# Contents

- [Docs](#Docs)
- [Tips](#Tips)
- [Vimrc](#Vimrc)
- [Vim Plugins Installed](#Vim Plugins Installed)
- [Plugins to consider](#Plugins to consider)
- [Vim Tricks](#Vim Tricks)
- [Switch case to lower](#Switch case to lower)
- [Upper and Lower Case](#Upper and Lower Case)
- [Tables](#Tables)
- [Append after visual block](#Append after visual block)
- [Registers](#Registers)
- [Marks](#Marks)
- [Tabs](#Tabs)
- [Quickfix](#Quickfix)
- [Moving Windows](#Moving Windows)
- [Macros](#Macros)

# Docs

* [vim docs](http://vimdoc.sourceforge.net/index.php)

# Tips

* [Vim - Today I Learned](https://til.hashrocket.com/vim)
* [vim wiki on Fandom](https://vim.fandom.com/wiki/Vim_Tips_Wiki)
* [Enabling Italics and Basics](https://rsapkf.netlify.app/blog/enabling-italics-vim-tmux)

# Vimrc
    * `<Leader>ev` - edit .vimrc
    * `ZZ or <Leader>wq` - save .vimrc and close vertical split
    * `<Leader>sv` - source .vimrc

# Vim Plugins Installed
    * [Pathogen instructions](https://gist.github.com/romainl/9970697) and [Tim's repo](https://github.com/tpope/vim-pathogen)
    * [vimwiki](https://vimwiki.github.io/)
    * [commentary](https://vimawesome.com/plugin/commentary-vim)
    * [markdown syntax](https://vimawesome.com/plugin/markdown-syntax)
    * [NERDTree]()
    * [vim-Flake8]()
    * [vim-latex]()
    * [tagbar](https://vimawesome.com/plugin/tagbar)
    * [csv-vim](https://vimawesome.com/plugin/csv-vim)
    * [vimux](https://github.com/benmills/vimux/blob/master/README.mkd) with bindings
    * [solarized](https://github.com/vim-scripts/Solarized) see note for Term users
    * [vim airline](https://github.com/vim-airline/vim-airline) with [powerline fonts](), https://powerline.readthedocs.io/en/master/installation/linux.html#fonts-installatio://github.com/powerline/fontsthough and additional status bar on top. there is also an apt package.
    * [vim airline themes](vimairline-theme://github.com/vim-airline/vim-airline-themes) there is also an apt package.
    * [tmuxline](https://github.com/edkolev/tmuxline.vim/blob/master/README.md) vim colors for tmux (see that tmux doesn't override it)
    * [fugitive](https://vimawesome.com/plugin/fugitive-vim) - git plugin
    * [vim pandoc markdown prepandoc view](https://github.com/conornewton/vim-pandoc-markdown-preview)
    * [vim cellmode](https://github.com/julienr/vim-cellmode) plugin for executing cells in IPython cli session. Copy-paste style.
      `C-c` selection.
      `C-g` current cell.
      `C-b` current cell and move to next.

# Plugins to consider
    * [vimproc](https://vimawesome.com/plugin/vimproc-vim)
    * [surround](https://vimawesome.com/plugin/surround-vim)
    * [tbone](https://vimawesome.com/plugin/tbone-vim)
    * alternative to vim-cellmode, there is [vim ipython](https://github.com/ivanov/vim-ipython/)
    * [vim markdown preview](https://github.com/JamshedVesuna/vim-markdown-preview) lets you live preview markdown in Chrome on buffer write
    * [or this one](https://github.com/iamcco/markdown-preview.vim)
    * [movements auto suggestions](https://github.com/AlphaMycelium/pathfinder.vim)

# Vim Tricks

remove blank lines in a file [source](https://vim.fandom.com/wiki/Remove_unwanted_empty_lines)
`:g/^$/d`

Count every stroke
http://www.vimgolf.com

bing your arrows to <Caps Lock>hjkl
https://askubuntu.com/questions/684459/configure-caps-lock-as-altgr-and-arrows-like-in-vim/898462#898462

test your setup with vanilla vim
`-u NONE` disables .vimrc
`-N` enabled no-compatible mode
`vim -u NONE -N`

source a different .vimrc file
`vim -u .custom_vimrc`

get shell access
`:sh`

Search forward to a char (ex: `+`), substitute it with space+space
`f+ s<Space>+<Space><Esc>`
Then simply `;.`

# Switch case to lower
whatever you select in visual mode you can convert with u or U
`vu`
or upper
`vU`
Toggle cases wihtout selecting
`~`
https://vim.fandom.com/wiki/Switching_case_of_characters



`:[range]w[rite] [++opt] !{cmd}`
Range is either `%` which means entire file or `'<,'>` which means visual selection
Send selection by email
`:%w !mutt -s “here are my notes” -- joe@example.com`
Running any external commands (shell commands):
you simply use `:!{cmd}`
[source](https://vimways.org/2019/vim-and-the-shell/)
`:!cat fruits.txt | awk '{sum += $2} END { print sum }'`
view a file in the same folder
[source](https://vim.fandom.com/wiki/Get_the_name_of_the_current_file)
`:!feh %:p:h/some-file.png &`


Insert Mode - Delete
del back one char `<C-h>`
del back one word `<C-w>`
del back to statt of line `<C-u>`

Insert Notmal Mode
from insert mode invoke normal mode for a one-off command
`<C-o>{cmd}`

Center Screen (vertivally) with current line in the middle
zz

Spell Check
changes are written to `.vim/spell/<lang-file>`

Folding
https://vim.fandom.com/wiki/Folding

Splits
Maximize current split - Width wise
`<Ctrl-w>|`
Maximize current split - Height wise
`<Ctrl-w>_`
Swap splits
`<Ctrl-w>R`
Resize all windows to equal dimensions based on their splits
`<Ctrl-w>=`
https://vim.fandom.com/wiki/Resize_splits_more_quickly
Help
`:help splits`

Buffers
`:bn` next
`:bp` previous
`:b` list
`bd #` delete buffer, where # is the number of the buffer (no # means current)
`:vert sb #` open a # buffer in a vertical split
https://vim.fandom.com/wiki/Buffers

Special Chars
display the char’s (under cursor) ascii code do `ga`
To enter the char from Insert mode do the hex code `<C-v>u{code}`
Or `<C-v>{code}` for ___ code
the other combination was.. `<C-k>{code}`

Moving
`<S-{>` and `<S-}>` moves you to the next paragraph
`<S-(>` and `<S-)>` moves you to the next sentence
`<[>` and `<]>` moves you to the next header _does it really work (?)_ yes, press it twice!
`ge` move to end of previous word

# Upper and Lower Case
`gU` - upper case
`gu`- lower case
`gUU` - on the whole line
`gUap` - around paragraph
`gR` - virtual replace mode that treats tab as multiple spaces
`gv` - select again the last visual selection

`o` - go to the other end of visual selection. E.g. toggle the free end

# Tables
Create horizontal line to separate table header
`yyp` - copy and paste first row of the table
`Vr-` - visually select this second line and replace each char with -

Reduce space between table columns
`<C -v>jjj`
`x...` - del one column of chars at a time

Add vertical line to separate columns
`gvr|` - select the same range again and replace with |

# Append after visual block
You can select multiple lines in visual block mode, from cursor to the end
`<C-v>jj$`
`A;` - Append `;` at the end of the selection in every line (at the end of selection, not end of line. End of line is only here because we used `$`)
`<Esc>`

# Registers

[more on registers](https://www.brianstorti.com/vim-registers/)

`"kyy` - copy the current line into register k

`"Kyy` - append to the `k` register by using a capital letter (K)

`"kp` - move through the document and paste it elsewhere

`"*y` to copy something to the clipboard register you type

`"*p` to put system clipboard into the editor

`"+p` - paste from system clipboard on Linux

`"*p` - paste from system clipboard on Windows (or from "mouse highlight" clipboard on Linux)

`:reg` - access all currently defined registers type

# Marks

[Using marks | Vim Tips Wiki | Fandom](https://vim.fandom.com/wiki/Using_marks)

`ma` set mark at current cursor location

`'a` jump to mark `a` at first non-blank char
``a` jump to mark `a` at line and column

`:marks` list current marks

`:marks aB` list marks a and B

# Tabs
:vimtabs:tabs:
[source](https://vim.fandom.com/wiki/Using_tab_pages)
`gt`            go to next tab
`gT`            go to previous tab
`{i}gt`         go to tab in position i


# Quickfix

`lopen` open qf window

files listed in qf window: using a plugin yssl/QFEnter you can open in splits:
`<leader><tag>` in new tab
`<leader><enter>` in vertical split (to the right)
`<leader><space>` in horisontal split (below the editor window)

You can also select in qf and with the motions above they will open in sequence.

# Moving Windows

`<C-w>HJKL` move to the extreme side (left, down, up, right respectively)

`<C-w>x` switch two windows which are next to each other

`:h window-moving` for more

# Macros

`q<key>` start recording a macro on the <key>. Ex: `qa` records the macro on `a`.

`q` stop recording macro.

`@<key>` trigger the macro recorded on the <key>. Ex: `@a` trigger macro from `a` key.

# Navigation

`gg` top of file.

`G` bottom of file.

Navigate using relative line number (set relativenumber).

`<num>jk` move to relative line number
