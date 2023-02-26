## Processing Delimited Files

CSVs are comma separated, and fields may or may not be surrounded by double quotes. The first line is often the header.

`cut -d',' -f1 csv-example.txt` extract just the first field. `-f1-3` provide a range of fields

`| tr -d '"'` and remove all quotes

`| tail -n +2` and remove header row. (eg. output starting from line 2)


### Iterating Through Delimited Data

If you want to extract fields line by line, `awk` is a better choice.

`awk -F "," '{print $4}' myfile.txt` where `","` is the quote-comma-quote separating fields

`grep "$(awk -F "," '{print $4}' myfile.txt)" anotherfile.txt` compare what's extracted against another file

### Processing by Char Position

If the fields (or some of them) in the file are fixed width, you can use `cut` with the `-c` option to extract by char position.

`cut -d',' -f3 myfile.txt | cut -c2-13 | tail -n +2` extract 3rd field, then extract chars from 2nd position, removing the quotes, then display without header row
