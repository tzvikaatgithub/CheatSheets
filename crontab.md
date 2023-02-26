CRONTAB
:cron:crontab:

This comman allows you edit the cron table on a linux system. The cron table is used to schedule tasks.

`-e` edit the cron table

`-l` list the current cron table

`-r` remove the current cron table

Example:
to run everyday at 8:00AM:
0 8 * * * /home/your-user/autoscan.sh

records in cron file contain fields:
    * `<min> <hours> <day of month> <day of week> <command>`
    * minutes can be 0-59
    * hours 0-23
    * day of month 1-31
    * month 1-12, January-December, Jan-Dec
    * Day of week 1-7, Monday-Sunday, Mon-Sun
    * (optional) binary to execute the script
    * command
