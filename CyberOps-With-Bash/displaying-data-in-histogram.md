## Displaying Data in a Histogram

The ability to draw a histogram is useful when you are looking over a large dataset.

see ~/scripts/bash-cyber/09-histogram.sh

This script takes two fields as the input, thus you can pipe 08-summer.sh to it. The first field will be the index of an associative array, and second as the value. It will iterate over the array and print it.

`cut -d' ' -f1,10 access.log | 08-summer.sh | 09-histogram.sh`

It will show you for example bytes of data transferred by IP address.

If you wanted to see dates and times, you can also draw it, after a little more processing (since the format contains extra chars):

`cut -d' ' -f4,10 access.log`  check format

`cut -d' ' -f4,10 access.log | tr -d '['` remove extra chars (or `cut -c2-`)

At this point you can extract just the date, ommiting the time, or extract just the time, ignoring the date. Either of these can provide interesting insights.

`sudo cut -d' ' -f4,10 /var/log/apache2/access.log.1 | cut -c14-15,22- | ./08-summer.sh | ./09-histogram.sh`

`-c2-` month, day, and year

`-c2-12,22-` entire date and time

`-c5-12,22-` month and year

`-c14-` full time

`-c14-15,22-` hour

`-c9-12-22-` year

Review the histogram of total amount of data that was retrieved on a certain day, hour by hour, sorted by numerical order:

`awk '$4 ~ "12/Nov/2017" {pprint $0}' access.log | cut -d' ' -f4,10 | cut -c14-15,22- | bash summer.sh | bash histogram.sh | sort -n`

