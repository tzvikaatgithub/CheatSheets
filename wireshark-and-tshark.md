WIRESHARK AND TSHARK
:wireshark:tshark:

`ssh root@<router-IP> -- "<tcpdump-command>" > <local-file.pcap>`Capture locally traffic from the router (zero config on router)

[wireshark cheat sheet](https://hackertarget.com/wireshark-tutorial-and-cheat-sheet/)
Wireshark can be useful for many different tasks, whether you are a network engineer, security professional or system administrator. Here are a few example use cases:
* Troubleshooting Network Connectivity
* Examination of Application Layer Sessions (even when encrypted by SSL/TLS)
* Troubleshoot DHCP issues with packet level data
* Extract files from HTTP sessions
* Extract file from SMB sessions
* Detect and Examination of Malware
* Examination of Port Scans and Other Vulnerability Scan types

[tshark cheat sheet](https://hackertarget.com/tshark-tutorial-and-filter-examples/)
tshark is a packet capture tool that also has powerful reading and parsing features for pcap analysis.

**Capture filters**: This type of filter is set before you start capturing traffic in Wireshark/Tshark. It cannot be changed while capturing traffic. It is generally used for capturing a specific type of traffic.

`tshark -f "${capture-filter}"`

**Display Filters**: This type of filter is used to reduce the number of packets shown in Wireshark/Tshark. This type of filter can be changed while capturing traffic.  It is generally used for hiding traffic to analyze the specific type of traffic.

`tshark -Y 'display filter'`  note the single quotes to avoid bash expansion



list available interfaces
`tshark -D`

capture packets on this interface
`tshark -i wlp4s0 -T fields -E separator=, -e eth.src -e eth.dst -e ip.src -e ip.dst -e ip.proto -e tr.src -e tr.dst -e frame.protocols -c 10 -w out-file.pcap -t ad`

`-T`  defines output format. -T fields means it shoudld be fields. You can also define other formats, such as json. When fields is defined as format, you can use -e option
`-E`  separator=,  sets comma as field separator in the output
`-e`  specifies fields to display (not limiting capture). Used together with -T fields
`-c`  is the number of packets to capture
`-w`  is write to file. Tip: write to a /tmp/ dir or Tshark might not like it even if you are root
`-t` ad  is to add a timestamp at the beginning
`-V`  dump the entire packet content
`-o`  format columns
`  `  For example, to print Wireshark's default columns with tshark:
    `tshark -o 'gui.column.format:"No.","%m","Time","%t","Source","%s","Destination","%d","Protocol","%p","Length","%L","Info","%i"'`
    so you'd add all your columns like this to format just one of them:
    `tshark -e columnA -e columnB columnC -o 'column.format:"columnA","%Yt","columnC"'`
`-f` 'capture-filter'   does not capture filtered out traffic
`-Y` "display.filter" defines a display fileter the way you would write it in wireshark filter field. Reduces the traffic displayed, after it was captured.


read pcap file
`tshark -r out-file.pcap`
`-z` hosts  this will pull out all dns resolutions





column formats
`tshark -G column.formats`


# RECIPIES

which URLs were loaded
`tshark -r out-file.pcap -T fields -e http.host -e http.request.uri -Y 'http.request.method == GET' | sort | uniq`

format to CSV output
`tshark -r sampleCapture.pcap -T fields -e frame.number -e ip.src -e ip.dst -e tcp.dstport -E header=y -E separator=, -E quoted -E occurrence=f > sampleCSV.csv`

`-E` specifies format options

`quoted=d` double quoted

`occurence=f` start from the first packet
