NETWORKING
:networking:

# Links

[basic networking commands](https://itsfoss.com/basic-linux-networking-commands/)
[ifconfig](https://www.computerhope.com/unix/uifconfi.htm)
[ip](https://www.computerhope.com/unix/ip.htm)
[netcat](https://www.tecmint.com/netcat-nc-command-examples/)

# Books

[Networking For Dummies](Networking-For-Dummies)



Find your DNS server IP
`cat /etc/resolv.conf`
DNS IP of a Website
`dig website.com`

View default gateway
`route -n`
location in Debian  _(?)_
`cat /etc/network/interfaces`
location in RHEL
`cat /etc/sysconfig/network-scripts/ifcfg-eth0`

View DNS settings
`nmcli dev show | grep DNS`
location  _(?)_
`cat /etc/resolv.conf`

[Network Monitoring Tools](http://www.linuxandubuntu.com/home/best-network-monitoring-tools-for-linux)

List netowrk adapters
[source](https://www.cyberciti.biz/faq/linux-list-network-cards-command/)
`lspci | egrep -i --color 'network|ethernet'`
`lshw -class network`
`iifconfig -a`
`ip link show`
`ip a`
`cat /proc/net/dev`
