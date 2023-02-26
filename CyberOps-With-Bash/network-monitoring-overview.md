How to monitor networks for configuration changes such as unexpected network services (open ports).

Monitor changes in open ports on systems throughout a network:
    1. read in a file containing IP addresses or hostnames
    2. for each host in the file, perform a network port scan for open ports
    3. save port scan output to a file named using the current date
    4. on next port scan, compare results to the last saved result and highlight any changes
    5. automate to the script to run on a daily basis and email admin if any changes occur

Note: the same can be accomplished using `Nmap Ndiff`
