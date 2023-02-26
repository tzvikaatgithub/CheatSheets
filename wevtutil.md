### WEVTUTIL
:win:wevtutil:

wevtutil is used to view and manage system logs in Win. You can call it from Git Bash.

[microsoft docs](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil)

`el` enumerate avail. logs

`epl` export log file. Ex: wevtutil epl System C:\backup\system0506.evtx

`qe` query a log's events

options:

`/c` specify the max # of events to read
`/c:1` - return only one log entry

`/f` format the output as text or XML
`/f:text` - return the result as plain text (not XML)

`/rd` read direction. If `true`, it will read the most recent logs first
`/rd:true` - read the most recent log entry

**note**: in Git Bash you will need to add a second forward slash before options `//c`

`wevtutil el` lists all of the avail. logs

`wevtutil qe System //c:1 //rd:true` view the most recent event in the System log via Git Bash

