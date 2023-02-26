:bash:read:

Read command enables you to read user input for your scripts.

It comes with a default `$REPLY` var, if you don't read user input into any var, it will set this one.

## Resources

* [Ryan's Tutorials](https://ryanstutorials.net/bash-scripting-tutorial/bash-input.php)
* [Bash read command](https://linuxhint.com/bash_read_command/)

## Intro

`read -p 'Username: ' uservar` provide (text) prompt before reading variable

`read -s passvar` **silently** read passvar variable from user input. No chars are displayed in the terminal when user types.

`echo 'give me 3 vars: '; read var1 var2 var3` read multiple variables

`read -n 5 -p 'What is your desired username?' username` limit number of input chars

`read -a array` store user input in an array:
    * `echo ${array[@]}` use as array

`read -t 3` set timeout

`read -r` do not allow `\` to be used as escape

## Intermediate

Pass multi-line to a var [source](https://stackoverflow.com/questions/1167746/how-to-assign-a-heredoc-value-to-a-variable-in-bash#1655389)
```
read -r -d '' VAR << EOF
first line
second line
third line
EOF
```

print VAR as multi-line - need to quote the var
`echo "$VAR"`
