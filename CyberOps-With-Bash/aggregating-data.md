## Aggregating Data

Before analysis, you must get all the collected data into one place and in a convenient format.

`find /data -type f -exec grep '{}' -e 'ProductionWebServer' \; -exec cat '{}' >> ProductionWebServer.txt \;` find all files in /data recursively, matching a regex and aggregate them

`>>` for each file we append it's data to the destination file

you can use `cp '{}' /destination-dir` instead of `cat` to copy over files

`join -t',' -2 2 1stfile.txt 2ndfile.txt` join two comma delimited files (space is default). Remember to `sort` files first

`-2 2` join  on second column of second file (first field is the default, in this case good for 1stfile.txt, otherwise use `-1 2 -2 2`)
