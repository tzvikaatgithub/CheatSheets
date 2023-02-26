# Braces
:bash:braces:

Braces `{}` group statements together
`[[ -d $DIR ]] || { echo "error: no such directory: $DIR" ; exit ; }`
it will only exit if dir doesn’t exist
Note: `if` isn’t necessary in the above case.
Braces can also be used to generate sequences according to the formula:
`{first..last..step}`
Most recent version of bash lets you pad digits with leading zeros
`{0xx..yy..zz}`
