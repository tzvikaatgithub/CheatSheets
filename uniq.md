### UNIQ
:uniq:

Filter out duplicate lines of data that occur **adjacent to one another**. Thus you must `sort` your file first.

    `-c` print out the number of times a line is repeated
    `-f` ignore the specified number of fields before comparing. Ex: `-f 3` will ignore the first three fields (delimited by space) in each line
    `-i` ignore case. By default uniq is case sensitive
