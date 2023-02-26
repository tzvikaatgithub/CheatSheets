FINDING UNIQUENESS IN DATA

1. identify (by IP) a system which was making a large number of page requests.
2. gain understanding of what it was doing on the server
3. categorize this activity as benign, suspicious, or malicious

Here is what can work for many data sets, despite that multiple passes are required
`awk '$1 == "192.168.0.37" {print $0}' access.log | cut -d' ' -f7 | bash countem.sh | sort -rn | head -5`

For extremely large datasets see
    * ~/Dropbox/configurations/scripts/bash-cyber/010-pagereq.sh
        - for newer versions of bash, using associative array (dict)
    * ~/Dropbox/configurations/scripts/bash-cyber/010-1-pagereq.awk
        - for older versions of bash, using awk instead of a dict
