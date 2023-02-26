TAR
:tar:

Tar Usage and Options

    `c` - create a archive file.
    `-C` - untar into a different (destination) dir (specified directory)
    `x` - extract a archive file.
    `v` - show the progress of archive file.
    `f` - filename of archive file.
    `t` - viewing content of archive file.
    `j` - filter archive through bzip2.
    `z` - filter archive through gzip.
    `r` - append or update files or directories to existing archive file.
    `W` - Verify a archive file.
    `p` - preserve permissions
    wildcards - Specify patterns in unix tar command.


[18 examples](https://www.tecmint.com/18-tar-command-examples-in-linux/)

create tar archive (not compressed)
`tar -cvf new-tar-ball.tar /path/to/dir/to/tarball/`
c – Creates a new .tar archive file.
v – Verbosely show the .tar file progress.
f – File name type of the archive file.
create compressed archive (with gzip)
`tar czvf new-tar-ball.tar.gz /path/to/dir/to/tarball/`
z - compresses the archive
create compressed archive (with bzip) - even smaller size
`tar cjvf new-tar-ball.tar.bz2 /path/to/dir/to/tarball/`

Uncompress tar
`tar -xvf public_html-14-09-12.tar`
untar into a different destination dir
`tar -xvf public_html-14-09-12.tar -C /home/public_html/videos/`
Uncompress tar.gz
`tar -xvf thumbnails-14-09-12.tar.gz`
Uncompress tar.bz2
`tar -xvf videos-14-09-12.tar.bz2`

List Content of tar Archive File
`tar -tvf uploadprogress.tar`
List Content tar.gz
`tar -tvf staging.tecmint.com.tar.gz`
List Content tar.bz2
`tar -tvf Phpfiles-org.tar.bz2`

Untar Single file from tar
`tar -xvf cleanfiles.sh.tar cleanfiles.sh`
Untar Single file from tar.gz
`tar -zxvf tecmintbackup.tar.gz tecmintbackup.xml`
Untar Single file from tar.bz2
`tar -jxvf Phpfiles-org.tar.bz2 home/php/index.php`

Untar Multiple files from tar, tar.gz and tar.bz2
`tar -xvf tecmint-14-09-12.tar "file 1" "file 2"`
`tar -zxvf MyImages-14-09-12.tar.gz "file 1" "file 2"`
`tar -jxvf Phpfiles-org.tar.bz2 "file 1" "file 2"`

Extract Group of Files using Wildcard
`tar -xvf Phpfiles-org.tar --wildcards '*.php'`
`tar -zxvf Phpfiles-org.tar.gz --wildcards '*.php'`
`tar -jxvf Phpfiles-org.tar.bz2 --wildcards '*.php'`

Add Files or Directories to tar
`tar -rvf tecmint-14-09-12.tar xyz.txt`
`tar -rvf tecmint-14-09-12.tar php`
Add Files or Directories to tar.gz and tar.bz2
`tar -rvf MyImages-14-09-12.tar.gz xyz.txt`
`tar -rvf Phpfiles-org.tar.bz2 xyz.txt`

How To Verify tar, tar.gz and tar.bz2
`tar tvfW tecmint-14-09-12.tar`
W - verify (the spelling!:)

Check the Size of the tar, tar.gz and tar.bz2
`tar -czf - tecmint-14-09-12.tar | wc -c`
`tar -czf - MyImages-14-09-12.tar.gz | wc -c`
`tar -czf - Phpfiles-org.tar.bz2 | wc -c`

Split Large ‘tar’ Archive into Multiple Files of Certain Size
https://www.tecmint.com/split-large-tar-into-multiple-files-of-certain-size/

Gathering Linux logfiles from `/var/log` (will require privileged access. eg. root or sudo)

`tar -czf ${HOSTNAME}_logs.tar.gz /var/log`

`-c` creates archive

`-z` compresses the resulting archive with gzip

`-f` specifies the file name

`HOSTNAME` var is automatically set by bash, and represents the current host (remote in this context). Added to the filename so we know from which system they came

# Make Backup of a dir
:backup:

[source](https://www.2daygeek.com/backup-user-home-directory-in-linux-using-tar-command/)

The script:

```bash
#!/bin/bash
DATE=$(date +%d-%m-%Y)
mkdir $HOME/boris
BACKUP_DIR="$HOME/boris"

#To backup 2daygeek's home directory
tar -zcvpf $BACKUP_DIR/boris-$DATE.tar.gz $HOME/Dropbox

#To delete files older than 10 days
# find $BACKUP_DIR/* -mtime +10 -exec rm {} \;
```

Put it on a cron:

`0 10 * * * /path/to/script.sh` every day at 10am
