### TR
:tr:

`tr` translate or map from one char to another. Often this is used to delete unwanted chars

It reads from stdin and writes to stdout

`-d` delete specified chars from input stream

`-s` squeeze (replace) repeaded instances of a char with a single instance

`tr '\\:'  '/|' < infile.txt  > outfile.txt` translate backslashes to forward slashes, and all colons to vertical bars

two backslashes are needed because `\` is used to indicate special chars such as newline `\n`, `\r` return, or `\t` tab

`''` single quotes around arguments avoid interpolations by bash

Windows files often come with both carriage return `\r` and linefeed `\n` at the end of the line, while Linux and MacOS systems have only newline at the end

`tr -d '\r' < Windowsfile.txt > fixedfile.txt` remove `\r` from the end of the line of a Windows files

`sed -i 's/$/\r/' Linuxfile.txt` add `\r` to the end of the Linux file

`echo -ne something\\r` where -n doesn't output new line, -e allows interpreting backslash and \\r is the return

`tr ';' '\t' < tasks.txt` translate all `;` in a file into a tab char

