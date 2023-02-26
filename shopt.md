SHOPT
:shopt:

available only bash 4.x+
`shopt -s lastpipe`
    here we `-s` set the command ran in the last pipe in the main script
    `firstcommand | something | else | lastcommand`
    firstcommand command will run in a subshell, but lastcommand in the main script/proc
