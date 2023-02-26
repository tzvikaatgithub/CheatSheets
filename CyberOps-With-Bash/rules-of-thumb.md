# Defensive Security Operations with Bash

Use command line to collect, process, analyze, and display data for defensive cybersecurity operations.

# Data Collection

Data tells us the current state of the system, what happened in the past, and what might happen in the future.


## Gathering System Info

To defend a system, you need to gather data, either locally or remotely, for analysis.


## Transferring Data

After you gather the data you will need to transfer it off the target system for analysis.

You can either copy it to a removable device or upload to a centralized server using Secure Copy.

`scp some_system.tar.gz bob@10.0.0.45:/home/bob/some_system.tar.gz` uploads the tar.gz file to the home dir on remote server

this can be added at the end of your collection script. Remember to give your files clear names.

do not include authentication passwords in your scripts, use ssh keys insted `ssh-keygen`

as a rule: gather all data you think might be relevant. you cannot analyze what you don't gather, but you can delete data later.

Before collecting data, first confirm that you have permission and legal authority to do so.

Adversaries often try to hide their presence by deleting or obfuscating data. To counter - use multiple methods of searching (file name, hash, contents, etc)


# Data Analysis

Start broad and continually narrow the search as new insights are gained into the data.







































