BASH
:bash:

The main value if the command line is not how well it can perform one particular task, rather how versatile and available it is.

# Books

[CyberOps With Bash](CyberOps-With-Bash/main)

[Learn Bash in Minutes](./LearnBash.sh)

[simple examples](https://www.ubuntupit.com/simple-yet-effective-linux-shell-script-examples/)

# Links

[How To Bash](../../../projects/pure-bash-bible/README)

[Many Bash Resources](https://github.com/awesome-lists/awesome-bash)

[Bash Reference Manual](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html)

[TLDR pages](https://tldr.sh/)

* [Very good rules for writing bash scripts](https://blog.yossarian.net/2020/01/23/Anybody-can-write-good-bash-with-a-little-effort)

* [Shell Productivity Tips](https://blog.balthazar-rouberol.com/shell-productivity-tips-and-tricks)

* [Bash Hackers Wiki](https://wiki.bash-hackers.org/)

* [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line)

* [Difference between $* and $@](https://eklitzke.org/bash-$%2A-and-$@)

* [Concurrency in Bash](https://ricardoanderegg.com/posts/bash_wrap_functions/) basically, put independent stuff in functions and run them with `&`

## Monitoring

Network monitoring
    * [article](https://linuxconfig.org/bash-scripts-to-scan-and-monitor-network)
    * [article]()https://linuxconfig.org/how-to-monitor-network-activity-on-a-linux-system


# Basics

:bash:env:

`#!/bin/bash` tells the script what executable to use. Assuming bash is in //bin/
`#!/usr/bin/env bash` - tries to solve portability issues. here `env` is used to look up the location of bash. Assuming env is in /usr/bin/

[Help messages for Bash scripts](https://samizdat.dev/help-message-for-shell-scripts/)

to run a script
`bash myscript.sh`
OR give it execute perms and run directly
```
chmod +x myscript.sh`
`./myscript.sh
```

print script absolute path
Linux
`"$(dirname "$(readlink -f "$0")")"`
Unix
`SCRIPTPATH="$( cd "$(dirname "$0")" >/dev/null 2>&1 ; pwd -P )"`

Open cli prompt in the default text editor
quitting the vim instance will execute whatever was typed in
`<C-x-e>`

Rename all files in current dir from .txt to .md
you need to install mmv
`mmv '*.txt' '#1.md'`

To list top 10 directories eating disk space in /etc/, enter:
`du -a /etc/ | sort -n -r | head -n 10`

Determine *encoding* of the file
`file -bi [filename]`
Change *encoding* of the file
`iconv -f [encoding] -t [encoding] -o [newfilename] [filename]`
Ex. convert from windows to linux
`iconv -f cp1251 -t utf-8 in.txt`
https://www.shellhacks.com/linux-check-change-file-encoding/

Terminal colors
`tput colors`

### DEBUG Bash Script

There are several ways to debug a Bash script step by step:

    Use the set -x option to enable the execution trace. This option causes the shell to print each command before it is executed.

```bash
#!/bin/bash
set -x
# Your script code here
```

    Use the bash -x command to run the script with the execution trace option enabled.

`bash -x script.sh`

    Use the echo command to print out the values of variables and the output of commands at different points in your script.

```bash
#!/bin/bash
# Your script code here
echo "Variable value: $var"
```

    Use the read command to pause the script execution at a certain point and inspect the state of the variables or the output of a command.

```bash
#!/bin/bash
# Your script code here
read -p "Press enter to continue"
```

    Use the bash -v command to run the script with the verbose option enabled. This option causes the shell to print each command after it is expanded but before it is executed.

`bash -v script.sh`

    Use a debugger such as bashdb which is a front-end to the GNU Debugger (GDB) for bash. It provides a command-line interface for debugging bash scripts.

`bashdb script.sh`

[BASH Debugger](https://bashdb.sourceforge.net/bashdb.html)

Using these methods, you can step through your script and inspect its behavior at different points, making it easier to identify and fix any bugs. It's also a good practice to test your script with different inputs and edge cases to ensure that it works as expected.

### Misc

Find real path of a file
`realpath myfile.sh`

Set alarm/timer to play music
`sleep 20m && rhythmbox myfile.mp3`

### I/O redirection

stdin is file descriptor 0
stdout is file descriptor 1
stderr is file descriptor 2 `2> errors.log`

stout and stderr (the standard behavior) `> results.out 2>&1`
shortcut for this: `&> results.out`

`myscript.sh < data.in  > results.out 2>&1`
this reads file data.in into myscript.sh as stdin
then it sends output to results.out instead of default stdout
and sends stderr to the same place as descriptor 1. `&1` stands for descriptor 1.
shortcut: `&> results.out` instead of `> results.out 2>&1`. eg. this sends both stdout and stderr to  results.out

tee command sends output to both the stdout and the file results.out
`muscript.sh < data.in | tee results.out`
tee has `-a` option, which appends to the results.out, instead of overwriting it

Append output to the file
`>> results.out`
`&>> results.out`

Discard output
`> /dev/null`

### JOBS

Run a job (process) in background [source](http://stackoverflow.com/a/37531889/1459669):

`&` puts the job in the background.

`disown` removes the process from the shell's job control, but it still leaves it connected to the terminal.

`nohup` disconnects the process from the terminal, redirects its output to nohup.out and shields it from SIGHUP.

`ping 8.8.8.8 > ping.log &`
the shell will continue to execute other commands without waiting for ping to finish.

Put a job in background
`<Ctrl>z` suspends the currently running in foreground job
`jobs` list jobs and their IDs
`bg %<ID>` places the job with ID from suspended state into background (and running)
`fg %<ID>` brings the job with ID from background into foreground

Store output of a command in a var
`CMDOUT=$(pwd)`
the command inside `$()` runs, and output is stored in the variable CMDOUT
this command runs in a sub-shell
inside the `$()` you can pipe multiple commands

Print output to the console (stdout)
```
echo something
echo "multiple words"
```
Substitution (expansion?)
```
echo 'no $CMDOUT substitution - single quotes'
echo "here $CMDOUT substitution takes place"
```
PrintF built in supports additional formatting
`printf "Hello World\n"`
ex:
`printf "%-15s %8d\n"  "${id}"  "${cnt[${id}]}"`
15 chars size for IP field
- sign means left justified
8 digits for the sum values
double quotes around params are a best practice to ensure they're treated each as one arg


# Monitoring Web Server

[source](https://linuxconfig.org/bash-scripts-to-scan-and-monitor-network)

[source](https://osric.com/chris/accidental-developer/2011/09/monitoring-web-server-status-with-a-shell-script/)

Monitoring script:
```
#!/bin/bash
if curl -s --head http://osric.com/ | grep "200 OK" > /dev/null
  then
    echo "The HTTP server on osric.com is up!" > /dev/null
  else
    echo "The HTTP server on osric.com is down!"
fi
```
Cron:
`crontab -e`
Every 5 minutes:
`*/5 * * * * /path/to/bash/script.sh`

# Optimizing Bash Speed

Built ins and keywords work a lot faster than compiled files and scripts that need an interpreter (especially in loops)

Find what the command is
`type -t <command>`

List available keywords, built-ins, and commands (files)
`compgen -k`  # example: if
`compgen -c`  # example: ls
`compgen -b`  # example: pwd

TODO compile a list of commands and their use with examples
