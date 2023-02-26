# Functions
:bash:func:

you can use either `function` or `();`
using both is more readable
```
function myfunc ()
{
  # body of the function goes here
}
```
Variables used in the func are global, unless declared with `local` built-in command.
`{}` are the most common way to group function body; all compound commands are allowed for that, but why would you want to run the func in a subshell..
I/O redirection on the func body (braces in this case) will do so for all the statements inside the func body.
No params are declared at func def. Whichever and however the params are passed on invocation get passed into the func.

Pass params to the func
`myfunc 2 /ara "14 years"`  # this passes 3 positional params

Params passed to func are referred to by `$1`, `$2`, etc, `$#`, which hides (masks) the args passed to the script which contains the func. To use script args inside func efficiently you need to save their values in a var. The only exception is $0, which keeps the script name, not func name.

Return values by default are 0 if all goes well, and non-zero if there was an error. Other values can be returned by either saving them to a var (which will be global by default) or printing them to stdout.  
Think of how you will use the function if it prints return values to stdout. It will either be a part of a pipeline or evaluated and the output saved. In both cases (examples below)

These funcs run in a subshell and the changes made to the global vars are lost!
```
myfunc args | next step | etc
RETVAL=$( myfunc args )
```

This func runs and saves the return value to a var:
```
function myfunc ()
{
    MYRES=“result stuff”
}
```

