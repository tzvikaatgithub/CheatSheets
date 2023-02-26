TCPDUMP
:tcpdump:

Note: tshark supports more protocol decoding than tcpdump.

`tcpdum -h` help

`tcpdump -D` list available interfaces

`tcpdump -i <interface>`
    `tcpdump -i any`

`tcpdump -n -i <interface>` display IP addresses and port numbers instead of domain names

`tcpdump -i any dst port 80` web traffic on any interface (displaying domain names)

`tcpdump -i any port 53` see if anybody is using DNS
    * useful to check for DNS leaks on VPN
    * or if you want to check that the devices are sending traffic where you want them to
    * `tcpdump -i <ppp0> -vv ip6` as is common for IPv6 to leak over VPN, you can check for it

`tcpdump -i any port 53 or port 80 or port 443` all web traffic

`tcpdump -i any host <internal-server-IP> and not src net <192.168.1.0/24>` ignore local traffic going to internal server
    * if you had a device (internal server or other) under suspicion of malware infection, you can monitor if anything connects to it

`tcpdump -i any dst net <local-net-IP/24> and not src net <local-net-IP/24>` check what connects to the whole network that is not coming from internal network

`tcpdump -i any -s 65535 -w capturefile.cap` capture to a file and limit size
