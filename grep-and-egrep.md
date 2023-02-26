## GREP and EGREP
:grep:egrep:

`grep` searches the content of the file for a given pattern and prints any line where the pattern is matched.

`grep -R -i 'pattern' /path` or: grep options pattern filenames

We will use the frost.txt [here](./) file.

Common grep options:

`-c` count number of lines that match the pattern

`-E` enable extended regular expression

`-f` read the search pattern from a file. The file can contain more than one pattern, one per line

`-i` ignore case

`-v` invert match (print whatever doesn't match the regex)

`-l` print only the names of files that contain the matches

`-L` print only the names of files that DO NOT contain the matches

`-I` print only the filename and path where the pattern was found

`-n` print the line number of the file where the pattern was found

`-h` suppress the output of filenames

`-P` enable the Perl regex engine

`-R`, `-r` recursively search subdirs

`--line-buffered` given to egrep to ensure that there are no command output buffering

There are 3 ways to tell grep that you want special meaning on certain chars:

1. by preceding those chars with a `\`
2. by passing `-E` to `grep`
3. by using `egrep` (which simply invokes `grep -E`)

## Misc

Regex to check spelling of words
`grep -i '^..j.r$' /usr/share/dict/words`
Major
major

Regex to validate email addresses
`"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"`
Get a list of email addresses from a file
`grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b" email-list.csv`

Regex to validate a phone number NOT matching the (xxx) xxx-xxxx format
`grep -Ev '^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$'`

Regex to find ugly file names (containing spaces)
`find . -regex '.*[^-_./0-9a-zA-Z].*'`
