# Looping
:bash:while:for:

all statements go between `do` and `done`
```
i=0
while (( i < 1000 ))
do
    echo $i
    let i++  # let executes i++ as an arithmetic expression
done
```

`break` this statement will break the loop

`continue` this statement skips over to the next interation of the loop

Simple numeric loop:
```
for ((i=0; i < 100; i++))
do
    echo $i
done
```

Iterating over arguments passed to the script:
```
for MYARG
do
    echo here is an argument: $MYARG
done
```

Looping over an arbitrary list of values:
```
for MYVAL in 20 3 dog peach 7 vanilla
do
    echo $MYVAL
done
```

list of values can be generated by output of other commands:
```
for MYVAL in $(ls | grep pdf) {0..5}  # list of pdf files and numbers 0 - 5
do
    echo $MYVAL
done
```

about `{}`
you can define a step `{start..finish..step}` and you can pad numbers with `0` like so `{001..100}`
and remember that `{}` group statements together

