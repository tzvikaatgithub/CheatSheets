# Contents

    - [Logic](#Logic)
- [Malware Hunting](#Malware Hunting)

:lsof:
[source](https://geekflare.com/lsof-command-examples/)

List Open Files. Find different processes locking up a file or directory, a process listening on a port, a user’s process list, what all files a process is locking.

Output fields:
    * `COMMAND  PID  TID  USER  FD  TYPE DEVICE  SIZE/OFF  NODE  NAME`
    * FD: file descriptor
        * possible values:
            * cwd  current working directory;
            * Lnn  library references (AIX);
            * err  FD information error (see NAME column);
            * jld  jail directory (FreeBSD);
            * ltx  shared library text (code and data);
            * Mxx  hex memory-mapped type number xx.
            * m86  DOS Merge mapped file;
            * mem  memory-mapped file;
            * mmap memory-mapped device;
            * pd   parent directory;
            * rtd  root directory;
            * tr   kernel trace file (OpenBSD);
            * txt  program text (code and data);
            * v86  VP/ix mapped file;
        * followed by:
            * r for read access;
            * w for write access;
            * u for read and write access;
            * space if mode unknown and no lock character follows;
            * `-' if mode unknown and lock character follows.
        * followed by LOCK char:
            * N for a Solaris NFS lock of unknown type;
            * r for read lock on part of the file;
            * R for a read lock on the entire file;
            * w for a write lock on part of the file;
            * W for a write lock on the entire file;
            * u for a read and write lock of any length;
            * U for a lock of unknown type;
            * x for an SCO OpenServer Xenix lock on part of the file;
            * X for an SCO OpenServer Xenix lock on the entire file;
            * space if there is no lock.
    * TYPE:
        * possible values: GDIR, GREG, VDIR, VREG, IPV4, IPV6 etc.

`sudo lsof | less` list all open files

`sudo lsof <file-name>` list all processes that have opened a specific file

`sudo lsof -u <user>` list all files opened by a specific user
    * `^<user>` can be used to negate

Kill all processes by a specific user
```
sudo kill -9 `lsof -t -u <user>`
```
    * `-t` show only PID

`sudo lsof -c <process-name>` list open files by process name

`sudo lsof -p <PID>` list open files by PID
    * `^<PID>` can be used for negation

`sudo lsof +D <path>` list processes that opened files under a specific dir.
    * `+D` does so recursively
    * `+d` does not include subdirs

`sudo lsof <options> -r<time-interval>` repeat at regular time interval
    * `-r` repeats until interrupted/killed
    * `+r` repeats until output has no open files

`sudo lsof -i` list open network connections

`sudo lsof -i -a -p <PID>` list all network connections in use by a specific PID

`sudo lsof -i -a -c <process-name>` list all network connections by a specific process name

`sudo lsof -i <protocol>` list open network connections by a specific protocol

`sudo lsof -i :<port>` list open network connections by a specific port number

`sudo lsof -i4` list open network connections by IPv4

`sudo lsof -i6` list open network connections by IPv6

`sudo lsof <path> | grep deleted` list deleted but locked files (using space, invisible by ls

## Logic

`lsof -u <user> -c <process-name>` multiple arguments with OR logic between them
`lsof -u <user> -c <process-name> -a` multiple arguments with AND logic between them

# Malware Hunting

`lsof -P -i`
    * `-P` list port numbers (without -P it will show https instead of 80)
    * `-i` list IP sockets
    * `-n` show IP addresses, not domain names
    * `-Pni` the `-i` should be the last one because we can add more to it
        - `-Pni4` show only IPv4
        - `-Pni6` show only IPv6
        - `-Pni4TCP` show only IPv4, TCP only
        - `-Pni4UDP` show only IPv4, UDP only
        - `-Pni4TCP:80` show only IPv4, TCP only, only on port 80
        - `-Pni4TCP:80,25` show only IPv4, TCP only, only on port 80 or 25
        - `-Pni4TCP@52.73.43.44:80` show only IPv4, TCP only, connecting to a specific IP on port 80

Check any listening ports that perhaps shouldn't have been listening (if you didn't use the process/service).

`lsof -P -i | grep -i listen` show only listening ports.

Check any established connections that perhaps shouldn't have been happening.

`lsof -P -i | grep -i establish` show only established connections.

`watch -dn1 lsof -Pni` watch differences continuously.

You can confirm results of lsof using nmap:
    * `lsof -Pni4TCP | grep -i listen` == `nmap -p1-65535 localhost`
