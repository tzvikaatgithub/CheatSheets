### TAIL
:tail:

`tail` outputs the last lines of a file, 10 by default

`-f` continuously monitor the file and output lines as they are added

`-F` make a `--retry` if the file is inaccessible

`-n` specify number of lines to output

`--pid` specify PID, if the process dies, tail will exit, you can specify `--pid=$$` to watch the current script. Useful for cleanup when the script runs in the background.

`tail -F logfile | egrep --line-buffered -i 'HTTP/.*" 404 | cut -d' ' -f-4-7' | tr -d '[]"'` search for 404s in the log file

`tail -F /var/logs/apache2/access.log | egrep --line-buffered -i -f ioc.txt | tee -a interesting.txt` monitor apache2 access log based on malicious patterns from ioc.txt, output and record in interesting.txt

ioc.txt can be populated by downloading regex for malicious patters here [IOCs and Indicators of compromise -download on Snort](https://www.snort.org/downloads)

wintail.sh is for windows :)
