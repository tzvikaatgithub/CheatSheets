### Positional params
:positional:params:$0:$1:$#:$@:$?:$!:

find more info in `man bash` and search for special parameters

`$0` holds the name of the script
`$1-$n` params separated by a space
`$#` number of params
`$@` All arguments, starting from first

`$?` exit status of the most recently executed foreground pipeline

`$_` At shell startup, it holds absolute path used to invoke the shell/shell script. Subsequently, last argument of the previous command in the foreground, after expansion.

`$-` current option flags as specified on invokation

`$$` PID of the shell. In a subshell it's the PID of the current shell, not the subshell

`$!` ID of the process most recently placed in the background

Positional arameters are assumed to be strings, with the first one being a built-in/script/executable name.

Some commands are able to do decimal calc, but bash itself wasn’t designed for that.
