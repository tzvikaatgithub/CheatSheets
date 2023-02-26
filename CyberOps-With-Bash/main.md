CYBEROPS WITH BASH

**Scripts dirs**:
    * ~/Dropbox/configurations/scripts/bash-cyber/
    * ~/Dropbox/projects/cyber-ops-with-bash/

[CIS Controls](https://www.cisecurity.org/controls/)
[IOCs and Indicators of compromise -download on Snort](https://www.snort.org/downloads)
    [rules explanation](https://www.snort.org/rules_explanation)

---
Foundations
---

# 1. CLI Primer

    Bash is a multitool, good general purpose, versatile, available everywhere.

    Git Bash - install on Win so you can run Bash commands.

    # SSH - install server on Win so you can access that machine. User is the Win user.

    **Script**: ~/Dropbox/configurations/scripts/bash-cyber/01-osdetect.sh

# 2. Bash Primer

[envs](envs)

[positional params](positional-params)

[user input](user-input)

[conditionals](conditionals)

[braces](braces)

[looping](looping)

[functions](functions)

# 3. Regex Primer

[pattern matching and regex](../regex-and-pattern-matching)

**Commands**:
    [grep and egrep](../grep-and-egrep)

# 4. Principles of Defence and Offence

[cyber security basics](cyber-security-basics)

---
Defensive Security Operations with Bash
---

# 5. Data Collection

[rules of thumb](rules-of-thumb)

**Commands**:
    Linux: [cut](../cut), [file](../file), [head](../head)
    Win: [reg](../reg), [wevtutil](../wevtutil)
    [ssh](../ssh), [scp](../scp), [tar](../tar)
    [gathering info commands](gathering-info-commands)
    [searching](../Find.md) <-.
                |
        [find](../Find) dir attrib egrep cut
        by time, size, content, type, hidden

# 6. Data Processing

**Commands**:
    [awk](../awk), [join](../join), [sed](../sed), [tail](../tail), [tr](../tr)

Processing files:
    [delimited files](delimited-files), [xml](xml), [json](../jq) and jq
    [aggregating data](aggregating-data)

# 7. Data Analysis

Commands:
    [sort](../sort), [uniq](../uniq)

[webserver access logs](webserver-access-logs)

[sorting and arranging data](sorting-and-arranging-data) sort, head

[counting occurrences in data](counting-occurrences-in-data) cut, awk

[totaling numbers in data](totaling-numbers-in-data) cut, sort

[displaying data in histogram](displaying-data-in-histogram) cut, awk

[finding uniqueness in data](finding-uniqueness-in-data)

[identifying anomalies in data](identifying-anomalies-in-data)

**Scripts:**
    ~/Dropbox/configurations/scripts/bash-cyber/07-countem.sh
    ~/Dropbox/configurations/scripts/bash-cyber/09-histogram.sh
    ~/Dropbox/configurations/scripts/bash-cyber/010-pagereq.sh
    ~/Dropbox/configurations/scripts/bash-cyber/010-1-pagereq.awk
    ~/Dropbox/configurations/scripts/bash-cyber/11-useragents.sh

# 8. Real-Time Log Monitoring

Logfiles can provide tremendous insight into the operation of a system, but they also come in large quantities, which makes them challenging to analyze. You can minimize this issue by creating a series of scripts to automate data formatting, aggregation, and alerting.

Commands:
    [trap](../trap), [shopt](../shopt)

[monitoring text logs](monitoring-text-logs)

[generating real time histogram](generating-real-time-histogram)

**Scripts:**
    ~/Dropbox/configurations/scripts/bash-cyber/12-wintail.sh tail for Win

    ~/Dropbox/configurations/scripts/bash-cyber/13-looper.sh loops and traps SIGUSR1
    ~/Dropbox/configurations/scripts/bash-cyber/14-tailcount.sh starts and stops counting and times the interval
    ~/Dropbox/configurations/scripts/bash-cyber/15-livebar.sh prints a real-time histogram

# 9. Tool: Network Monitor

Early detection of adversarial activity.
    [network monitoring overview](network-monitoring-overview)


[port scanner](port-scanner)

[comparing previous output](comparing-previous-output)

[automation and notification](automation-and-notification)

Commands:
    [crontab](../crontab), [schtasks](../schtasks), [printf](../printf), tempfile

Scripts:
    ~/Dropbox/configurations/scripts/bash-cyber/16-scan.sh scans ports on a specified host
    ~/Dropbox/configurations/scripts/bash-cyber/17-fd2.sh compare latest and previous scan, output diff
    ~/Dropbox/configurations/scripts/bash-cyber/18-autoscan.sh runs the other two scripts and emails user on any changes


# 10. Tool: Filesystem Monitor

[System Baseline Overview](system-baseline-overview)

TODO:

detecting-changes-to-the-baseline


Commands:
    [sdiff](../sdiff)

Scripts:
    ~/Dropbox/configurations/scripts/bash-cyber/19-baseline-filesystem.sh


# 11. Malware Analysis

Commands:
    curl, vi, xxd

# 12. Formatting and Reporting

Commands:
    tput

---
Penetration Testing with Bash
---

# 13. Reconnaissance

Commands:
    ftp

# 14. Script Obfuscation

Commands:
    base64, eval

# 15. Tool: Command-Line Fuzzer

# 16. Establishing a Foothold

Commands:
    nc

---
Security Administration with Bash
---

# 17. Users, Groups, and Permissions

Commands:
    chmod, chown, getfacl, groupadd, setfacl, useradd, usermod, icacls, net

# 18. Writing Log Entries

Commands:
    eventcreate, logger

# 19. Tool: System Availability Monitor

Commands:
    ping

# 20. Tool: Software Inventory

Commands:
    apt, dpkg, wmic, yum

# 21. Tool: Validating Configuration

# 22. Tool: Account Auditing
