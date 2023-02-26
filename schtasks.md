SCHTASKS
:win:schtasks:

This command allows you to schedule tasks to run commands at a particular time or interval on a Windows system

We need to schedule Git Bash to run and give it the autoscan.sh file as an argument.

To schedule autoscan.sh to run every day at 8:00 AM on a Windows system:

`schtasks //Create //TN "Network Scanner" //SC DAILY //ST 08:00 //TR "C:\Users\Paul\AppData\Local\Programs\Git\git-bash.exe C:\Users\Paul\autoscan."`

The path to Git Bash must be accurate.
Because of Git Bash we are using double forward slashes. In Win cmd it would be only one slash.

`//Create` create a new task

`//Delete` delete a scheduled task

`//Query` list all scheduled tasks

`//TN` task name

`//SC` Schedule frequency. Valid values are:
    MINUTE
    HOURLY
    DAILY
    WEEKLY
    MONTHLY
    ONCE
    ONSTART
    ONLOGON
    ONIDLE
    ONEVENT

`//ST` start time

`//TR` task to run
