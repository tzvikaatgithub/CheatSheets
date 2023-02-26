AUTOMATION AND NOTIFICATION

the following script just needs to be added to a cron or a scheduled task

~/Dropbox/configurations/scripts/bash-cyber/18-autoscan.sh

`crontab -l`

`crontab -e`

to run everyday at 8:00AM:
0 8 * * * /home/your-user/autoscan.sh

this needs chmod +x on the file, otherwise you'd need to run it wiht bash autoscan.sh
