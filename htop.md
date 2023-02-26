# Contents

- [Uptime](#Uptime)
- [Load Average](#Load Average)
- [Processes](#Processes)
    - [PID](#Processes#PID)
    - [Process Tree](#Processes#Process Tree)
    - [Process User](#Processes#Process User)

:htop:

* [Htop](https://peteris.rocks/blog/htop/)

# Uptime

How long the system had been running.
    * you can use `uptime` to get this info
    * the info comes from `/proc/uptime`, which gives two numbers:
        1. total number of seconds
        2. idle (this one is a sum for multiple cores, so it can be greater than the 1st
    * you can see which files the uptime program opens using `strace uptime 2>&1 | grep open`

# Load Average

The same command `uptime` gives you load average by reading `/proc/loadavg`.

There are four columns:
    1. system load at last 1 minute period
    2. system load at last 5 minute period
    3. system load at last 15 minute period
    4. number of currently running processes, over the total number of processes
    5. last PID used:
        - PID 1 is the /sbin/init, started at boot time

Load average is distributed over the number of your CPUs. If your setup can run 2 processes at any given time, and the average is 1 process, then the CPU utilization is 50%.

# Processes

Processes are called Tasks in htop, this is internal kernel taxonomy. Also it's shorter.

Threads can be toggled on and off with `<S-H>`. Kernel threads with `<S-K>`.

## PID

In bash each job is assigned a PID. You can view the last job using `echo $!`.

`procfs` is a pseudo file system that allows programs to get info from the kernel by reading it's files.
    * Usually it is mounted in `/proc/`. Each process will be in `/proc/<PID>`
    * if you want to know which command launched that PID, do `cat /proc/<PID>/cmdline`
    * `/proc/<PID>/cwd` points to the current working dir
    * `/proc/<PID>/exe` points to the executed binary

## Process Tree

Toggle with `<F5>`.

This functionality is available also in cli using `ps -f`.

Child processes are created in bash using the fork system call. It makes a copy of bash, and runs a process in it. Parent usually waits for the child to exit.

The boot process has a PID of 1. It spins up other processes.

## Process User
