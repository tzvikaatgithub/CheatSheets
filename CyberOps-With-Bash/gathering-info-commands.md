# Gathering a Variety of Info

Data is needed for forensic investigations, verifying compliance, and detecting malicious activity.


|------------------|------------------------------|--------------------------------------------|
|                  | Data of Interest             |                                            |
|------------------|------------------------------|--------------------------------------------|
| Data             | Data Descrition              | Data Location                              |
|------------------|------------------------------|--------------------------------------------|
| Log files        | Historical system activity.  | Linux: /var/log                            |
|                  | Web and DNS server logs,     | Win: Event Log                             |
|                  | router, firewall, IDS logs,  |                                            |
|                  | application logs             |                                            |
|------------------|------------------------------|--------------------------------------------|
| Command history  | Recently executed commands   | Linux: `echo $HISTFILE`                    |
|                  |                              | `cat ~/.bash_history`                      |
|------------------|------------------------------|--------------------------------------------|
| Temp files       | User and system files,       | Linux: `/tmp`, `/var/tmp`, `echo $TEMPDIR` |
|                  | that were recently accessed, | Win: `c:\windows\temp`                     |
|                  | saved, or processed          | `%USERPROFILE%\AppData\Local\`             |
|------------------|------------------------------|--------------------------------------------|
| User Data        | Docs, pictures, other        | Linux: `/home/`                            |
|                  |                              | Win: `c:\Users\`                           |
|------------------|------------------------------|--------------------------------------------|
| Browser History  | Recently visited Web pages   | dep on OS and Browser                      |
|------------------|------------------------------|--------------------------------------------|
| Windows Registry | Hierarchical DB of settings, | Windows Registry                           |
|                  | other critical Win data      |                                            |
|------------------|------------------------------|--------------------------------------------|

## Linux

Common log files on Linux are located in:

* `/var/log/apache2/` apache webserver - access and error logs
* `/var/log/auth.log` info about user logins, privileged access, and remote authentication
* `/var/log/kern.log` kernel logs
* `/var/log/messages` generic non critical system info
* `/var/log/syslog` general system logs

more info about logs can be found in `/etc/syslog.conf` or `/etc/rsyslog.conf` on most distros

## Win

Win Registry is a repository of settings that define how the system and apps will behave.

Often registry key values can be used to identify the presence of malware and other intrusions.

`regedit //E ${HOSTNAME}_reg.bak` - Export the entire Windows registry `//` is b/c Git Bash; Win cmd only needs one

`reg export HKEY_LOCAL_MACHINE $(HOSTNAME)_hklm.bak` - export a section of the registry or a sub key

|---------------------|---------------|-----------------------------------|
| Linux               | Win Git Bash  | Description                       |
|---------------------|---------------|-----------------------------------|
| `uname -a`          | `uname -a`    | OS version                        |
|---------------------|---------------|-----------------------------------|
| `cat /proc/cpuinfo` | systeminfo    | system hardware info and more     |
|---------------------|---------------|-----------------------------------|
| `ip/ifconfig`       | `ipconfig`    | network interface info            |
|---------------------|---------------|-----------------------------------|
| `route`             | `route print` | routing table                     |
|---------------------|---------------|-----------------------------------|
| `arp -a`            | `arp -a`      | Address Resolution Protocol table |
|---------------------|---------------|-----------------------------------|
| `netstat -a`        | `netstat -a`  | list network connections          |
|---------------------|---------------|-----------------------------------|
| `mount`             | `net share`   | list filesystems                  |
|---------------------|---------------|-----------------------------------|
| `ps -e`             | `tasklist`    | list running processes            |
|---------------------|---------------|-----------------------------------|

