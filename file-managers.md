:file:managers:

# netrw

:netrw:

Netrw is a part of (neo)vim.

[Vim: you don't need NERDtree or (maybe) netrw | George Ornbo](https://shapeshed.com/vim-netrw/)

`Explore` opens browser directly in the buffer

`Vexplore` vertical split

`Sexplore` horizonal split

`i` cycle through the views (there are 4)

    `let g:netrw_linestyle = <nb>` set a default view

`let g:netrw_banner = 0` remove banner

`let g:netrw_winsize = 25` set width to 25%

`let g:netrw_browse_split = <1-4>` set how files are opened

    * `1` in new horizontal split
    * `2` in a new vertical split
    * `3` in a new tab
    * `4` in previous window

`%` Create file directly from file browser view

# nnn

:nnn:

[nnn is an excellent command line based file manager for Linux, macOS and BSDs- gHacks Tech News](https://www.ghacks.net/2019/11/01/nnn-is-an-excellent-command-line-based-file-manager-for-linux-macos-and-bsds/)
 NAVIGATION
         Up k  Up                PgUp ^U  Scroll up
         Dn j  Down              PgDn ^D  Scroll down
         Lt h  Parent            ~ ` @ -  HOME, /, start, last
     Ret Rt l  Open                    '  First file
         g ^A  Top                  . F5  Toggle hidden
         G ^E  End                     0  Lock terminal
         b ^/  Bookmark key            ,  Pin CWD
          1-4  Context 1-4        (B)Tab  Cycle context
            /  Filter                 ^N  Nav-as-you-type toggle
          Esc  Exit prompt            ^L  Redraw/clear prompt
            ?  Help, conf              +  Toggle proceed on open
            q  Quit context           ^G  QuitCD
           ^Q  Quit                    Q  Quit with err
 FILES
         o ^O  Open with...            n  Create new/link
         f ^F  File details            d  Detail view toggle
           ^R  Rename/dup              r  Batch rename
            z  Archive                 e  Edit in EDITOR
     Space ^J  (Un)select           m ^K  Mark range/clear
         p ^P  Copy sel here           a  Select all
         v ^V  Move sel here        w ^W  Copy/move sel as
         x ^X  Delete                  E  Edit sel
            *  Toggle exe
 MISC
         ; ^S  Select plugin           =  Launch app
         ! ^]  Shell                   ]  Cmd prompt
            c  Connect remote          u  Unmount
         t ^T  Sort toggles            s  Manage session

VOLUME: 135.061G of 466.309G free

NNNLVL: 1
SELECTION FILE: /home/george/.config/nnn/.selection


# Ranger

:ranger:

python based
