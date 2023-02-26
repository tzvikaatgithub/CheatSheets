MUTT

:mutt:

[source](https://www.tecmint.com/send-mail-from-command-line-using-mutt-command/)

[Mutt docs](https://www.mutt.org/doc/manual/)

[Mutt wiki](https://gitlab.com/muttmua/mutt/-/wikis/home)

[Arch Linux - Mutt docs](https://wiki.archlinux.org/index.php/Mutt)

[Gmail config example](https://gist.github.com/jaysonrowe/2624926)

Vim style key bindings:
    * [muttrc](https://github.com/pigmonkey/dotfiles/blob/master/config/mutt/muttrc)
    * [key bindings](https://github.com/pigmonkey/dotfiles/blob/master/config/mutt/vim-keybindings.rc)
    * [print to PDF](https://github.com/pigmonkey/dotfiles/blob/master/config/mutt/print.sh)
    * [ArchLinux wiki](https://wiki.archlinux.org/index.php/Mutt#Key_bindings)

[Viewing Docs and PDFs](https://raymii.org/s/articles/Viewing_PDF_docx_and_odt_files_in_Mutt.html)

`mutt` cli UI

`mutt -h` short help

# Nomenclature

Emails are identified by 3 states:
    `N` New - message is new and unread (indicated by a N in the first column of the index)
   ` O` Old - message is old and unread (indicated by an O in the first column of the index)
    Read - message has been presented to the user (nothing in the first column of the index)
   ` r` replied

Filtering message view
    [available patterns](http://www.mutt.org/doc/manual/#patterns)
    `l` this command allows you to add a filter
        `~U` or `unread` all unread
        `~R` or `read` all read
        `~A` or `all` return to view all messages
        `~N` or `new` new messages
        `~O` or `old` old messages
        `=b <string>` search imap server for message body containing string
        `=B <string>` the whole message containing string
        `~s <string>` messages with a specified subject (in this case pizza
        `~L <expr>` to or from or cc or bcc
        `~f <expr>` from
        `~X [min]-[max]` with min-max attachments
        `all` to view all messages unfiltered, or to remove filter


# Navigation

Gmail style navigation:
    `j` to move down.
    `k` to move up.
    `d` to delete a message
    `y` to archive one
    `gi` to view your Inbox
    `ga` to view All Mail
    `gd` to view Drafts
    `gs` to view Starred messages

Mutt specific navigation:
    `c` lets you change to a different folder
        `c` start changing to a different folder
        either type `?` to view a list of all your tags and folders
        or prepend your tag with an equals sign
        Ex: to view messages tagged 'work', you'd type `c`, then `=work`, then hit Return
    `/` lets you search the current folder
    `$` process commands
        some commands are not actioned right away, instead they are saved for later processing
        `$` applies all commands
    `<number><enter>` jump to msg number in the list

Inside Email Message:
    `<space>` scroll down
    `-` scroll up
    `i` go back to list

Sending mail
    `m` for new mail
    `r` reply to mail
    enter recipients, subject etc
    save message
    `y` send mail
    `R` recall postponed message

Moving messages to a different folder:
    You need to save it to a different folder
    you can tag multiple messages and save them
    `t` will mark a message
    `s` will save one, or more
        `s` start saving message to a folder
        `=work` save to 'work' folder
        if you use `t` to mark a bunch of messages, the operation will apply to all of them

`q` quit mutt

# Config

Config is stored in `.muttrc`
```
# Gmail configs
set imap_user = "your.email@domain.com"
set imap_pass = "YourPassword"
set smtp_url = "smtp://your.email@smtp.gmail.com:587/"
set smtp_pass = "YourPassword"
set from = "your.email@gmail.com
set realname = "Your Name"

set editor = "nvim"
```

External links:
    %% install urlview
    %% add .urlview with couple lines of config
    %% urlscan is better than urlview, it doesn't clip long URLs
    install urlscan
    add .urlvscan with couple lines of config
    add <C>-u config into .muttrc

HTML emails:
    install w3m
    add .mailcap with convig override (one line)

Set dynamic vars:
    old way:
    `set editor=echo \$EDITOR`
    new way:
    `set editor=$EDITOR`

Signature:
    place signature file in .mutt/
    point signature var to it in .muttrc

Solarized
    place repo in .mutt/
    source the theme you want in .muttrc

# Macros

Macros Guide: [Macros · Wiki · Mutt Project / mutt · GitLab](https://gitlab.com/muttmua/mutt/-/wikis/MuttGuide/Macros)

Functions you can call: [The Mutt E-Mail Client](https://muttmua.gitlab.io/mutt/manual-dev.html#functions)

# Printing

muttprint package is used for fancier printing

`p` print message

# cli UI
`mutt -s "Test Subject" recepient@example.com` this also opens interface
    `t` - change recipient email address
    `c` - change Cc address
    `a` - attach file
    `q` - quit cli UI
    `y` - send email; it will show status

# CLI

`mutt <options> <recipient>`
    `-s "My Subject"` - add subject
    `-c <cc-recipient@example.com>` - add Cc
    `-b <bcc-recipient@example.com>` - add BCc
    `-a <file>` add attachment file

In my setup, there are .muttrc , .mailcap , and .w3m/<some-files> that are used (mailcap and keymap)
