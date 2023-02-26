# Contents

- [Resources](#Resources)
    - [OpenBSD](#Resources#OpenBSD)
    - [MacOS](#Resources#MacOS)
    - [Other](#Resources#Other)
- [PF cli](#PF cli)
- [PF GUI](#PF GUI)
- [Little Snitch](#Little Snitch)

PF firewall (Packet Filter)

:pf:macos:openbsd:firewall:

# Resources

## OpenBSD

* [OpenBSD PF: User's Guide](https://www.openbsd.org/faq/pf/)
    * this ^ set of documents is a supplement to [pf(4) - OpenBSD manual pages](https://man.openbsd.org/pf)
* [Does Your Mac Really Need a Firewall? What You Need to Know](https://www.makeuseof.com/tag/mac-really-need-firewall/)
## MacOS

* Apple's application firewall page https://support.apple.com/en-us/HT201642
* Old OS X PF Manual from Murus http://murusfirewall.com/Documentation/OS%20X%20PF%20Manual.pdf
* Using pf on OS X Mountain Lion http://blog.scottlowe.org/2013/05/15/using-pf-on-os-x-mountain-lion/

## Other

* Wikipedia - PF Firewall https://en.wikipedia.org/wiki/PF_%28firewall%29
* Pf Firewall Tutorial https://calomel.org/pf_config.html
* Apps and Processes that are exempt from `standard` firewalls:
    * `sudo defaults read /System/Library/Frameworks/NetworkExtension.framework/Resources/Info.plist ContentFilterExclusionList`

# PF cli

PF is disabled by default on Macos, enabled by default on OpenBSD.

Main config file:
    * `sudo vim /etc/pf.conf`
    * there are others though, so each app can load it's own conf file with rulesets.

Different parts in pf.conf:
    * Macros: user defined vars
    * Tables: structure to hold IP addresses
    * Options: control how PF works
    * Filter Rules: allow selective filtering or blocking of packets as they pass through the interfaces.
        * can give params for NAT and packet redirection

`pfctl` is the tool to control the packet filter (PF) and network address translation (NAT) device.

Anchors are files with collections of rules, you will see the default osx anchor file loaded through the main config file by default. You can add your own, although osx will complain.
`anchor "my.file.pf"`
`load anchor "my.file.pf" from "/etc/pf.anchors/my.file.pf.rules:`

Inspect rules:
    * `pfctl -sr` show current rule set
    * `pfctl -ss` show current state table
    * `pfctl -si` show filter stats and counters
    * `pfctl -sa` show everything it can

`sudo pfctl -v -n -f /etc/pf.conf` test config file (it loads custom anchors too)

`sudo pfctl -v` put firewall in verbose mode

`sudo pfctl -e` enable firewall
    `-E` gives a token, as it increments the pf enable reference count

`sudo pfctl -d` disable firewall

`sudo pfctl -f <file>` load new rules (after changes)

If you inspect the default apple anchor file, you will see that it loads a custom ApplicationFirewall anchor. The built in ApplicationFirewall generates a dynamic set of rules and loads them with `sudo pfctl -e` (`-f`?).

`sudo pfctl -a com.apple/250.ApplicationFirewall -s rules`
    * `-a` point to the anchor
    * `-s rules` see the rules

More info: `man pfctl`

[internet guide with more info](./pf.html)


# PF GUI

Murus is the best, it also includes Vallum, which is Application based firewall. Has great docs and vids.


Software
pflist
http://www.hanynet.com/pflists/index.html
Icefloor
http://www.hanynet.com/icefloor/
Murus
http://www.murusfirewall.com/
Vallum
http://vallumfirewall.com/

# Little Snitch

Software
Littlesnitch
https://www.obdev.at/products/littlesnitch/index.html
