INFO COMMANDS

:man:
`man command` - the full manual

`man man` learn how to use man page

:apropos:

`apropos <search-term>` search all available names and descriptions of commands

:whatis:
`whatis command` - short description. Traverses a set of databases with short descriptions provided by the user and prints out system commands that match them.
    * Sometimes you get two descriptions.

:help:
`command --help` - longer description


:type:

:which: search for the absolute path of executables on the system
`which` display the first executable path found
`which -a` display all executable paths found

:whereis:
`whereis <binary>` if typed by itseld, gives 3 absolute paths - binary, source code, manual
    `whereis -b` absolute path of the binary only
        `-B` specify dirs to look in

    `whereis -s` source code
        `-S` specify dirs to look in

    `whereis -m` manual
        `-M` specify dirs to look in
    `whereis -l <binary>` provide a detailed list of all paths

