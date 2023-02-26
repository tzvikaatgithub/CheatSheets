:rootkits:rkhunter:chkroot:

# Contents

- [Rkhunter](#Rkhunter)
- [Chkrootkit](#Chkrootkit)

Check also ClamAV

# Rkhunter

`rkhunter` checks for rootkits and more. Siggnature based tool.

`rkhunter --update` first update it.

`rkhunter --versioncheck` compares your version to the latest.

`rkhunter --propupd` set baseline in a file.

`rkhunter -c --enable all --disable none` do all checks and don't ignore any (that's a lot of checks). Usually this is added as a cron to run on a server.
    * `--rwo` if you append this to the command, you will get only the warnings, not all output

`vim /etc/rkhunter.conf` - configuration file. Uncommend and add whatever you need.

`rkhunter -C` check configuration file for validity.
    * after this run all checks again to make sure there are no false positives
    * after all is in order you want to run the command to set the baseline again

# Chkrootkit

`chkrootkit -l` see available tests.

`sudo chkrootkit` check your system.
