GENERATING REAL TIME HISTOGRAM

We will write two scripts:
1. line counter: count how many lines added to a file
2. timekeeper:   watch the clock (eg. during a given time interval)

Timekeeper will notify Linecounter using a standard POSIX interprocess comms mechanism - signal.

Signal is a software interrupt. Some are fatal (terminate a proc). Most can be ignored or caught, and an action be takeb. Many have a predefined purpose.

We will use SIGUSR1 (one of the two avail. to users, the other one is SIGUSR2).

`trap` is a shell cmd to catch interrupts sent to a proc

take a look at ~/Dropbox/configurations/scripts/bash-cyber/13-looper.sh which loops and traps SIGUSR1

[how to send signals to a proc](https://bash.cyberciti.biz/guide/Sending_signal_to_Processes) - if you want to test it ;)

take a look at ~/Dropbox/configurations/scripts/bash-cyber/14-tailcount.sh which starts and stops counting, and times these intervals

take a look at ~/Dropbox/configurations/scripts/bash-cyber/15-livebar.sh which prints a histogram based on tailcount and looper output


