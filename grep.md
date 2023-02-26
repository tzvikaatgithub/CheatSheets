# GREP
:grep:

[nice grep resource](https://www.howtoforge.com/tutorial/linux-grep-command/)

`cat Regans-QA-Data-pulled-from-Engineering-Portal.csv | grep -E '^([0-9]{4}-[0-9]{2}-[0-9]{2},[[:alpha:]]{2} [[:alpha:]]{1,})'`
count 14 digit IMEIs
`cat  Regans-QA-Data-pulled-from-Engineering-Portal.csv | grep -E '^([0-9]{4}-[0-9]{2}-[0-9]{2},[[:alpha:]]{2} [[:alpha:]]{1,},[[:digit:]]{0,},[[:digit:]]{4}-[[:digit:]]{2}-[[:digit:]]{2} ([[:digit:]]{2}:){2}[[:digit:]]{2},[[:digit:]]{14})' |wc -l`

search for string recursively in files
`grep -inr 'string' /path/to/dir/`

:zgrep:

Zgrep can be used on zip files or files compressed using the gzip

`zgrep <pattern> file.gz`

`zgrep <pattern> file.gz file-within-archive-to-search` search only specific files within the archive

`zgrep <pattern> file.gz -x file-within-archive-to-exclude-from-search` exclude specific files within the archive from being searched
