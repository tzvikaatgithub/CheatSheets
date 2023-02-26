:io:input/output:
:file:descriptors:

Each proc gets 3 file descriptors:

    * STDIN - /proc/<processID>/fd/0
    * STDOUT - /proc/<processID>/fd/1
    * STDERR - /proc/<processID>/fd/2

There are also shortcuts:

    * STDIN - /dev/stdin or /proc/self/fd/0
    * STDOUT - /dev/stdout or /proc/self/fd/1
    * STDERR - /dev/stderr or /proc/self/fd/2

`fd` is file descriptor.

Useage in scripts: `cat salesdata.txt | myscript.sh`

And here is the script:

```
    #!/bin/bash
    # A basic summary of my sales report
    echo Here is a summary of the sales data:
    echo ====================================
    echo
    cat /dev/stdin | cut -d' ' -f 2,3 | sort
```
All we do here is:
    * print a header
    * `cat` the file descriptor for stdin
    * `cut` sets space as delimiter, keeping fields 2 and 3
    * sort output
