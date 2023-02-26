PROCESSES

:proc:process:management:
:ps:top:kill:crobtab:at:
[systemctl](service)
[crontab](crontab)

:boot:order:
[Stages of Linux booting process - explanation, step by step tutorial](https://www.crybit.com/linux-boot-process/)
[How to Run a Linux Program at Startup with systemd](https://www.howtogeek.com/687970/how-to-run-a-linux-program-at-startup-with-systemd/)

Process is a program that runs on your computer.

Daemon is a process that runs continuously.

Thread is a set of multiple processes that are related.

Job is like a work order.

Script is a file with commands.

Filesystem: [/proc](https://opensource.com/article/20/4/proc-filesystem)

# PS

`ps -ef` list all processes, you need to filter by process name

`ps -u <gdm> -U <user>` List processes from a single user

list processes of multiple users:
    * `ps -u gdm -U gdm -u root -U root`
    * `pgrep -l -u gdm -U gdm -u root -U root`

`ps -aef | grep avahi` filter processes based on username

# TOP

Top tells you about the system resources.

`top -u gdm` List processes from a single user. Top accepts either `-u` or `-U` but not at the same time

# Kill

`kill <PID>` kill a process by process ID

# AT

`at` is an ad hoc scheduler
