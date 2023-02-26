# Conditionals
:bash:if:

`$?` stores success/failure value. each command returns a success (true) or failure value, despite whether it produces output or not.
`0` No news - good news. True, success. The logic is that it is zero error.
`1` or `-1` or other non-zero values indicate a failure, false. The logic is - on error, return the error code.
```
#!/bin/bash
# extended conditional

count=99
if [ $count -eq 100 ]
then
    echo "Count is 100"
elif [ $count -gt 100 ]
then
    echo "Count is greater than 100"
else
    echo "Count is less than 100"
fi


if cmd | another-cmd | last-cmd
then
    success-cmd
else
    else-cmd
fi
```
Only the last-cmd in the pipe determines what the `if` takes as success or failure.
WARNING :-) `wc` alsways produces success, don't pipe into it when checking for truth

You can use the compound command `[[` or the built-in `[` or `test` to check for truth
```
if [[ -e $FILENAME ]]
then
    echo $FILENAME exists
fi
```
More options for `if [[ -`:
`-d` Test if a directory exists
`-e` Test if a file exists
`-r` Test if a file exists and is readable
`-w` Test if a file exists and is writable
`-x` Test if a file exists and is executable
Numeric tests:
`if [[ $FRSTVAR -lt $SNDVAR ]]`
`-eq` Test for equality between numbers
`-gt` Test if one number is greater than another
`-lt` Test if one number is less than another

Caution: `<` only compares alphabetical order (even for numbers), so 12 < 2 is true

Note: if you want to use `<`, you can do it with `((`. As it assumes everything is a number, not string. You don't need `$` inside the `((` construct, unless it’s a positional argument, so not to confuse `$1` with the actual 1.
Here, empty or unset vars are evaluated to 0.
Inside `((` 0 is false, everything else is true. This is the opposite of all other if statements, where 0 is true and all else is false. Therefore:
`if (( $? )) ; then echo "previous command failed" ; fi`

