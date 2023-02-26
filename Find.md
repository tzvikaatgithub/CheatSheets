# FIND
:find:

find searches dirs from the specified and recursively down and locates files matching a specific criteria. Actions can be defined to act on the matches

find uses *tests*, *options*, and *actions* to identify files
`find [path] -type [type] -name [“pattern”] -size [size]`

# Tests
there is a large number of tests, a few examples below
`find ~ -type f -name “*.JPG” -size +1M`

## Types:
`b` - Block special device file;
`c` - Character special device file;
`d` - Directory;
`f` - Regular file;
`l` - Symbolic link (lower case L)

# Name Pattern
it’s best to enclose in double quotes, to prevent pathname expansion

# Size:
leading + sign indicates we are looking for something larger than that. Leading - sign means smaller. Using no leading sign would mean the exact size match. Trailing M means megabytes
## Size Units:
`b` - 512-byte blocks. This is the default if no unit is specified.
`c` - Bytes
`w` - 2-byte words
`k` - Kilobytes (units of 1024 bytes)
`M` - Megabytes (units of 1048576 bytes)
`G` - Gigabytes (units of 1073741824 bytes)

# Operators
operators allow you to introduce logical relationships between tests
expressions are evaluated from left to right. This means the second expression (after -or) is not always evaluated. It is done for performance improvement, so if not necessary, the second expression is not evaluated
`find ~ \( -type f -not -perm 0600 \) -or \( -type d -not -perm 0700 \)`
## Operators:
`-not;` !
`-or` `-o`
`-and` `-a` this is the default, it’s implied when no operator is present
`( )` - groupings. Note that you need to escape parentheses with backslashes

# Actions
## Predefined Actions:
`-delete` Well.. delete the file
`-ls` This is the equivalent of “ls -dils” which is sent to stdout
`-print` Default action, which outputs the full path name to stdout
`-quit` Quit once found a match
there are many more. Take a look at man find
## User-Defined Actions:
`-exec` [command] { } ;  here { } represents the current pathname and ; is indicating the end of the command. Braces and semicolon delimiter must be single quoted ‘{}’ ‘;’ if placed plainly on the command line
`-ok`. you can use -ok instead of -exec if you want to be promoted for confirmation
`find ~ -type f -name 'foo*' -ok ls -l '{}' ';'`

in the above examples, the action is executed on every match as a separate command. Below are some ways to execute one command on all matches, which is more efficient (works for commands that accept filename multiple parameters, such as ls)

# Executing commands on results of find
## Built-in function to execute parameters as one command
substitute the trailing semicolon for a + sign
`find ~ -type f -name 'foo*' -exec ls -l '{}' +`
## Using Xargs to build a command from stdin
xargs accepts input from standard input and converts it into an argument list for a specified command
`find ~ -type f -name 'foo*' -print | xargs ls -l`

# Handling Spaces in Filenames
using `-print0` (to print null char after every file name) and  `--null` (to accept null delimited stdin arguments)
`find ~ -iname '*.jpg' -print0 | xargs --null ls -l`
find files and dirs with bad permissions and change them
`find ~ \( -type f -not -perm 0600 -exec chmod 0600 '{}' ';' \) -or \( -type d -not -perm 0700 -exec chmod 0700 '{}' ';' \)`

# Options
options control the depth of the scope of the fine command. There are many options, here are some common ones:
`-depth` - this tells find to process files before directories. This is the default when -delete action is specified
`-maxdepth` [levels] - Set max number of levels that find will descend into the directory tree when performing the search
`-mindepth` [levels] - Set min number of levels that find will descend when performing the search
`-mount` - don’t traverse dirs that are mounted on other filesystems
`-noleaf` - do not optimize for Unix-like filesystem search. Useful when searching DOS/Windows filesystems and CD-ROMs

# Examples

Rename all files in current dir (removing 4 first chars. In my case the chars `./` got added to the beginning, so files became hidden)
`find ./ -type f -name '.-*.pdf' -exec rename -n 's/.{4}(.*)/$1/' {} \;`
`-n` option is for verbose testing. If you remove it, rename will do the job for real.
# Searching the Filesystem

`find /home -name '*password' 2>/dev/null` search recursively in /home for file ending in password

in Windows replace /home with `/c/Users`

`-iname` makes the search case insensitive

`'*password'` is a shell pattern, not a regex

 `2>/dev/null` suppresses errors

in Linux you can find *Hidden* files by searching for `'.*'` eg. those that start with a period

in Windows *hidden* files are designated by a file attribute:

`dir c:\ /S /A:H` cmd command to identify hidden files on Win

`/S` traverse recursively

`/A:H` display files with hidden attribute

Git Bash intercepts `dir` and runs `ls` insted, therefore we need to use `find`:

`find /c -exec attrib '{}' \; | egrep '^.{4}H.*' | cut -22-`

`attrib` is a Win command, which displays (sets/removes) file attributes; without params it displays them

`{}` will be replaced with the pathname of the files that are found

`\;` semicolon terminates the command

`| egrep '^.{4}H.*'` pipe to egrep and print only where the 5th char is `H` (eg. hidden attribute is set)

`| cut -c22-` -c option tells cut to use chars, starting from position 22 (start of file path), and continue until the and of the line (`-`)

the last additon will allow you to pipe this path somewhere else


# Searching by Filesize

identify unusually large files, or the largest or smallest file on the system:

`find /home -size +5G` files greater than 5 gigs

`find / -type f -exec ls -s '{}' \; | sort -n -r | head -5` largest 5 files

`ls -s` displays the size in blocks, the blocks are listed first, so they can be sorted

`head -5` displays top 5, the largest, to get the smallest use `tail -5`, or remove `-r` (reverse) from `sort`

same can be achieved in a much more efficient way (ls vs find):

`ls -R -s / | sort -n -r | head -5`


# Searching by Time

Find files that were last accessed or modified

`find /home -mmin -5` files modified less than 5 min. ago

`find /home -mtime -1` files modified less than 24 hours ago.

`-mtime` takes number of days `1` is 1 day and a sign `-1` means less, `+1` means more than 1 day, unsigned number `1` means exactly

if you `cp` files that `find` finds, make sure they are *NOT* in the path where `find` is searching, or it will find the copies and copy them over again.

`find /home -type f -name abc*.txt -exec cp '{}' /home/myuser/copies/ \;` this is what *NOT* to do!


# Searching for Content

`grep -i -r /home -e 'password'` search for case insensitive recursively in /home and the regex pattern should match the word password

`-n` displays the line in file

`-w` matches only the whole words

(very heavy combination of commands, not a good idea to run as a background task:)  
`find /home -type f -exec grep 'password' '{}' \; -exec cp '{}' ./ \;` find and copy over to current dir


# Searching by File Type

`file` command identifies file types by comparing contents of the file. It uses magic numbers. Some common ones are found at file offset 0 bytes

see ~/scripts/bash-cyber/05-typesearch.sh for a script that looks for files of specific types (matching them using regex)

lightweight version of this search:

`find / -type f -exec file '{}' \; | egrep 'PNG' | cut -d' ' -f1`

XXX `file` depends on the `/usr/share/misc/`, which can be modified by a malicious user. Run it from a secure uncompromized system.


# Searching by Message Digest Value

hashing algo produces a message of fixed length, also called 'digest'.

only the content is evaluated, the file name does not affect the hashing algo.

see ~/scripts/bash-cyber/06-hashsearch.sh which uses a SHA-1 hashing algo to search the system recursively for a known digest.

`b2sum` - currently only BLAKE2 is available on Ubuntu.

`find /data -type f -exec grep '{}' -e 'ProductionWebServer' \; -exec cat '{}' >> ProductionWebServer.txt \;` find all files in /data recursively, matching a regex and aggregate them
## Aggregating Data

Before analysis, you must get all the collected data into one place and in a convenient format.

`find /data -type f -exec grep '{}' -e 'ProductionWebServer' \; -exec cat '{}' >> ProductionWebServer.txt \;` find all files in /data recursively, matching a regex and aggregate them

`>>` for each file we append it's data to the destination file

you can use `cp '{}' /destination-dir` instead of `cat` to copy over files

`join -t',' -2 2 1stfile.txt 2ndfile.txt` join two comma delimited files (space is default). Remember to `sort` files first

`-2 2` join  on second column of second file (first field is the default, in this case good for 1stfile.txt, otherwise use `-1 2 -2 2`)
