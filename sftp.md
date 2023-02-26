SFTP

:scp:sftp:

# SCP

SCP was the older tool, now phased out.

`scp some_system.tar.gz bob@10.0.0.45:/home/bob/some_system.tar.gz` uploads the tar.gz file to the home dir on remote server

[Deprecating scp [LWN.net](https://lwn.net/SubscriberLink/835962/ae41b27bc20699ad/)
Use the following instead:
    * [sftp](https://geekflare.com/sftp-command-examples/)
    * rclone
    * rsync

# SFTP

[How to Use Mac Terminal as FTP or SFTP Client | Beebom](https://beebom.com/how-to-use-mac-terminal-ftp-sftp-client/)

Basic idea:
    * login: `sftp -P <port> <user>@<url>`
    * add file: 'put </local/path/to/file> <remote/path/to/file>'
    * rename: `rename <old> <new>`
    * download: `get <remote> <local>`
