:netstat:

# Contents

- [References](#References)
- [Switches](#Switches)

# References

* FreeBSD [32.2. Gateways and Routes](https://www.freebsd.org/doc/handbook/network-routing.html)
* restarting network on Macos `sudo ifconfig en0 down; sudo ifconfig en0 up` or look up the interface with `ifconfig -a`

# Switches

`netstat -rn`
    * `a` show all connections and listening ports
    * `-p` pid  owning process - helps to identify process that causes the connection. This will add PID/Program name column
    * `-r` show routes
    * `-n` resolve IPs
    * `-t` tcp
    * `-u` udp
    * `-l` listening
    * `-e` ethernet stats on sent/received data. Flow info.
    * `-0` idengify process using a connection. Gives you a PID

Win switches:
    * `b` process name
    * `o` process ID

Columns:
    * Proto, Recv-Q, Send-Q, Local Address,          Foreign Address, (state)
    * Proto - protocol used
    * Local connection - from which machine
    * Foreign Address - destination:port
        * :https - means port 443
    * State:
        * Established - means ongoing connection
        * Listening - connection is listening on local port
    * Flags - shows info about the route stored as binary choices
        - USGs - route usable, dest requires forwarding, route added manually, proto-specified generate new routes on use

 1       RTF_PROTO1       Protocol specific routing flag #1
 2       RTF_PROTO2       Protocol specific routing flag #2
 3       RTF_PROTO3       Protocol specific routing flag #3
 B       RTF_BLACKHOLE    Just discard packets (during updates)
 b       RTF_BROADCAST    The route represents a broadcast address
 C       RTF_CLONING      Generate new routes on use
 c       RTF_PRCLONING    Protocol-specified generate new routes on use
 D       RTF_DYNAMIC      Created dynamically (by redirect)
 G       RTF_GATEWAY      Destination requires forwarding by intermediary
 H       RTF_HOST         Host entry (net otherwise)
 I       RTF_IFSCOPE      Route is associated with an interface scope
 i       RTF_IFREF        Route is holding a reference to the interface
 L       RTF_LLINFO       Valid protocol to link address translation
 M       RTF_MODIFIED     Modified dynamically (by redirect)
 m       RTF_MULTICAST    The route represents a multicast address
 R       RTF_REJECT       Host or net unreachable
 r       RTF_ROUTER       Host is a default router
 S       RTF_STATIC       Manually added
 U       RTF_UP           Route usable
 W       RTF_WASCLONED    Route was generated as a result of cloning
 X       RTF_XRESOLVE     External daemon translates proto to link address
 Y       RTF_PROXY        Proxying; cloned routes will not be scoped

# Examining Connections

When sysdig is not available..

* Any connection you don't understand what it is should be traced back to the process that started it.
* Any endpoints you are not sure what they are, check their IP, find out who they are, think whether you should be conencting to that IP

`netstat -aon | more`
    * `-a` all
    * `-o` timer
    * `-n` numeric output. If you don't pass it, it will show domain name (at least in part).
    * `-c` continuous (refreshing)
    * check your OS netstat version for exact flags
        - ex: in Unix, `-p <proto>` is used to define a protocol

Foreign address 0.0.0.0:* means nowhere. It is usually a local service listening.

`netstat -atp` all tcp with PID/Program name

`netstat -atp | grep -i listen` only listening tcp
    * same as `netstat -ltp` but `-l` is better, because grepping for 'listen' fails to pick out those that don't have the STATE column set

`netstat -aup | grep -i listen` only listening udp
    * `-l` is better as per the above

`netstat -luptn` listening udp PID tcp numeric

`watch -d -n0 "netstat -atp | grep -i ESTA"` better way to display continuous refresh (because it refreshes for all processes).

`netstat -tn 2>/dev/null | grep :80 | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr | head` IP addresses with high numbers of connections

`netstat -tn 2>/dev/null | grep ':80' | awk '{print $5}' | sed -e 's/::ffff://' | cut -d: -f1 | sort | uniq -c | sort -nr | head` IP addresses connected on port 80

`netstat -antu | grep :80 | grep -v LISTEN | awk '{print $5}'` list just the foreign IPs with ':80' in it

Best to use netstat as root :).
