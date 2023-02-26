:python:pdb:debugging:

Set breakpoint before executing your code
```
import pdb; pdb.set_trace
# your code
```

a newer and better way, which does both actions at once and also uses env var PYTHONBREAKPOINT when it is =1
`breakpoint()`

after running the file it will stop at the breakpoint
`ll` list function's source (show where you are

`n` continue execution until the next line

`s` execute the current line and stop at the first opportunity

`p my_var` print variable

`p <any-valid-python-expression>`
