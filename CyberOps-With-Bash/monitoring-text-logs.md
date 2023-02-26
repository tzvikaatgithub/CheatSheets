MONITORING TEXT LOGS

The ability to detect malicious activity as it happens is as important as to be able to extract info from a logfile after an event.

`tail -F logfile | egrep --line-buffered -i 'HTTP/.*" 404 | cut -d' ' -f-4-7' | tr -d '[]"'`

you can then pipe the output into grep or egrep, buffering lines so that each line is output to stdout as soon as a line break occurs, otherwise it will be buffered and only output when buffer is filled

(Normally buffering is used because I/O calls are more expensive than searchng for text)

the option `-i` ignores case

and piped to `cut` to clean the output

and then piped to `tr` to remove the square brackets and orphan double quotes


[IOCs and Indicators of compromise -download on Snort](https://www.snort.org/downloads)

`tail -F logfile | egrep --line-buffered -i -f ioc.txt | tee -a suspicious.txt`

you can compare the output of tail command against a file ioc.txt containing suspicious patterns. Webserver patterns are too numerous, more examples can be downloaded from Snort ^

Windows doesn't have an equivalent to `tail`, so we will use a bash cript the achieve the same result:

~/Dropbox/configurations/scripts/bash-cyber/12-wintail.sh
