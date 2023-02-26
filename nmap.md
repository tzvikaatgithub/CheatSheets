NMAP
:nmap:

# Contents

- [Resources](#Resources)
- [Basics](#Basics)

# Resources

* [Nmap - Best Network Monitor and Port Scanner Tool - GBHackers](https://gbhackers.com/information-gatheri-using-nmap/amp/)
* [cheat sheet](https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/)
* [see all devices on network](https://www.howtogeek.com/423709/how-to-see-all-devices-on-your-network-with-nmap-on-linux/)

# Basics

nmap is Cross platform, easy, fast. It can discover open ports, view running services, and fingerprint the OS.

`man nmap` network exploration tool and secruity / port scanner.
    * can identify OS
    * there are examples at the bottom
    * there is also Options Summary

`ifconfig` find the network and cidr

Ping Sweep:
    * `nmap -sP <IP/cidr>` find what other hosts are on the network and what services they are running

TCP Connect Scan:
    * `nmap -sT <IP/cidr>`
    * this is noisy
    * you can slow it down by using `-T0`

Stealth (SYN) Scan:
    * `nmap -sS <IP/cidr>`
    * the results are the same as TCP Connect Scan
    * slower and stealthy

Fingerprinting:
    * `nmap -O <IP/cidr>`

Scan for Known Vuln:
    * `nmap -sV -p 443 --script=ssl-heartbleed <IP/cidr>`
    * uses a built in script

`nmap -sV -O -sS -T5 <target-IP>` versions scanning on hosts
    * version
    * stealth scan
    * across the entire range of the host
    * OS fingerprint
    * T5 timing

Scan and find devices on the network (also see resources)
`sudo apt-get install nmap`

`ip a show <interface>`

Find your local network range

`nmap -sP <192.168.1.0/24>` ping scan and syn scan

`nmap -T4 <192.168.1.0/24>` regular port scan

`namp -T4 -F <network/subnet 192.168.1.0/24>` note the 0 for device
    * `-T<#>` timing template number - 4 is fast execution
    * `-F` fast mode, fewer ports than the default scan
    * `-A` OS detection
    * `-v` verbose

`nmap -O <target-IP>` identify OS of the target
    * it makes requests and receives responses.
    * Depending on how the target responds, it makes assumption about the OS on it

`nmap -sV <target-IP>` identify services and their versions
    * it does banner grabs and response packet analysis
    * `-s` service
    * `-V` version

`nmap -sS <target-IP>` syn scan

`nmap -sT <target-IP>` full connect scan
    * does 3-way handshake

`nmap -sA <target-IP>` acknowledgement scan
