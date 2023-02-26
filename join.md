### JOIN
:join:

`join` combines lines of two files that share a common field. To work, input files must be sorted.

`-j` join using the specified field number (fields start at 1)

`-t` Specify the char to use as the field separator (delimiter)

`--header` use the first line of each file as a header

`join -1 3 -2 1 -t, accesstime.txt usernames.txt` join on 3rd column in first file and 1st column in second file, using `,` as a separator

