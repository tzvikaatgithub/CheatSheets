RSYNC
:rsync:

# Intro

rsync can be used instead of scp. It syncs files or dirs between servers, or local to remote and back.

# Download

Download file from remote to local via ssh:

`rsync -avzhe ssh user@remote:/path/to/dir /local/path`

# Basic Usage

`rsync source destination`

Sync one dir to another dir:

`rsync -vrplogDtH /old/usr/local/apache/conf /usr/local/apache`
    * `-v` verbose
    * `-r` recursive
    * `-p` preserve permissions
    * `l` copy symlinks as symlinks
    * `-o` preserve owner
    * `-g` preserve group
    * `-D` preserve device files
    * `-t` preserve modification times
    * `-H` preserve hard links

That will sync the /old/usr/local/apache/conf/ directory to the /usr/local/apache/conf/ directory on the same server.


Sync dirs over ssh:

`rsync -ave ssh root@192.168.0.1:/backup/ /backup/`

That will take the backup directory on 192.168.0.1 and copy it to the server the command is run from. The command will also accept a remote destination if you adjust the command line accordingly.
