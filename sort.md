### SORT
:sort:

Rearrange a text file into numerical and alphabetical order. ASC by default, starting with numbers and then letters, Upper case first.

`sort -k 1.5,1.7 myfile.txt` sort using chars 5-7 of the first field, dot notation makes it a subset
    `-r` sort in descending order
    `-f` ignore case
    `-n` use numerical ordering (1, 2, 3, .. , and only then 10; in alphabetical it is 10, 2, 3)
    `-k` sort based on a subset of the data (key). Fields delimited by whitespace
    `-o` write output to a file
