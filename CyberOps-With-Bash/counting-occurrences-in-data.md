## Counting Occurrences in Data

A webserver log can contain thousands of entries. First count occurrences. Ex: how many times a page was accessed, or which IP address requested the page.

* High number of requests returning 404 (Page Not Found) for a specific page - broken hyperlinks
* High number of requests from a single IP returning 404 - probing activity
* High number of requests returning 401 (Unauthorized), particularly from a single IP - attempt to bypass authentication (brute-force)

To detect this we need to extract source IP, and count occurrences.

See ~/scripts/bash-cyber/07-countem.sh which counts occurrences (without sorting them)

To use - pipe any logfile field into it: `cut -d' ' -f6 logfile.log | bash 07-countem.sh`

Another way to pipe based on a condition: `awk '$9 == 404 {print $6}' logfile | bash 07-countem.sh`

the difference between this and `| grep something` is that using awk you can limit that to checking a specific field, while grep just checks anywhere in the line

and you can test multiple fields `awk '$4 == "PCI:" && $3 != "kernel:" {print $4}' dmesg | bash ~/scripts/bash-cyber/07-countem.sh`

at the end you can pipe it to sort `| sort -rn` (reverse, numeric)

Analyze webserver access log:

1. `cut -d' ' -f1 access.log | bash 07-countem.sh | sort -rn` find which host accesses the server the most (or `cut -d' ' -f1 access.log | sort | uniq -c | sort -rn`)
2. `awk '$1 == "192.168.0.37" {print $0}' access.log | cut -d' ' -f7 | bash 07-countem.sh` this will give you a count of requests for each page. Obviously use the IP of the host from step 1 :)
3. `awk '$1 == "192.168.0.36" {print $0}' access.log | cut -d' ' -f12-17 | uniq` take a look at the user-agent of a suspicious host
