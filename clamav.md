CLAMAV

:clamav:clamscan:freshclam:

# Setting up on Mac
[source](https://redgreenrepeat.com/2019/08/09/setting-up-clamav-on-macos/):
1. Install using brew
2. copy freshclam.conf.sample to freshclam.conf
3. edit and comment the Example line

# virusscan script
it excludes Google Drive
```
today_date=$(date +%Y-%m-%d)
clamscan --infected --bell --exclude ~/Google*/ --recursive / --log ~/tmp/virusscan-"$today_date".out
tail -20 ~/tmp/virusscan-"$today_date".out
```

Earlier versions used to want you to do freshclam but now it does it automatically

Script to scan dir or file as param
    * note the "$1" is quoted to avoid issues with dir names that have spaces
```
#!/usr/bin/env bash
if [[ $1 && -d $1 ]] || [[ $1 && -f $1 ]] ; then
    clamscan --infected --bell --exclude ~/Google*/ --recursive "$1"
else
    echo 'Usage: scandir <dir-or-file>'
fi
```

:rootkit:
[source](https://www.tecmint.com/scan-linux-for-malware-and-rootkits/)

`sudo lynis audit system`

`sudo chkrootkit`

`sudo rkhunter -c`

`freshclam; clamscan -r -i <dir>`

[LMD](https://www.tecmint.com/install-linux-malware-detect-lmd-in-rhel-centos-and-fedora/) integrates with clamav
