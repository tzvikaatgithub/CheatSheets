### CUT
:cut:

cut reads a file line by line (separated by a delimiter into fields, default is tab) and extracts select portions from it. Fields start at position 1.

`cut -d' ' -f2 file.txt` extract second field, delimited by space, from each line
    `-c` specify chars to extract
    `-d` specify delimiter (default - tab)
    `-f` specify fields to extract.

Ex: `cut -d',' -f1-3,5` extracts fields 1-3 and 5

Caveats:

* using a space as delimiter in files where there are varying number of spaces between fields
