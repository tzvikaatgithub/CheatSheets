### FILE
:file:

file command identifies a given file's type. It does so by analyzing the first block of data in the file.

`file unknownfile`

`-f` read the list of files to analyze from a file

`-k` list all matches for the file type (not just the first)

`-z` look inside compressed files

`-h` don't follow symlinks

`-p` preserve date of access to file, to pretend that file command never read it.

