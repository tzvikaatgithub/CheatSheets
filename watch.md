WATCH
:watch:

`watch` execute a program periodically, showing output fullscreen

`watch -d -n1 lsof -Pni`
    * `-d` show differences between successive updates
        - differences are **highlighted**
        - Gotcha: if the output is larger than the screen, you might not see the updates
    * `-n1` interval of seconds

You cannot use `| grep something` with `watch`, it doesn't work

