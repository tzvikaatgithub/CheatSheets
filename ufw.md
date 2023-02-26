# Contents

- [Basics](#Basics)
- [VPN Kill Switch](#VPN Kill Switch)
    - [Script](#VPN Kill Switch#Script)
    - [Manual Tasks](#VPN Kill Switch#Manual Tasks)
        - [Disable IPv6](#VPN Kill Switch#Manual Tasks#Disable IPv6)

:ufw:

# Basics

* [How To Set Up a Firewall with UFW on Ubuntu 20.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04)
`ufw allow from <Remote-IP> to <local-IP>`

`ufw enable`

`ufw status verbose`

`ufw allow 53`

`ufw allow 22/tcp`

`ufw allow 21/udp`

`ufw deny 8080/tcp`

`ufw delete <deny 8080/tcp>` delete rule

`less /etc/services` list services by name

`ufw allow <service-name>`

# VPN Kill Switch

:vpn:killswitch:

## Script

Note:
    * our script will reset any predefined rules, so it sets it's own sane defaults
    * we must allow the VPN gateway when we define killswitch:
        * reason: if the killswitch is on, and vpn is off, vpn must be able to connet to it's gateway to establish connection
        * problem: those gateways are dynamic, our script must determine their IPs on the fly
        * solution [security - UFW: Allow traffic only from a domain with dynamic IP address - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/91701/ufw-allow-traffic-only-from-a-domain-with-dynamic-ip-address#91711)
        * Macos important: you need to change the order of services [Can't access network resources over VPN connection on Mac OS X | InterWorks](https://interworks.com/blog/jpoehls/2012/04/18/cant-access-network-resources-over-vpn-connection-mac-os-x) AND hit "Apply" button.
    * IPv6 needs to be disabled on:
        * the system level
        * the ufw firewall level
        * in VPN configuration
    * We also want to check which operating system we are using, and which firewall tool is available to us

Sources:
    * [Linux - source](https://thetinhat.com/tutorials/misc/linux-vpn-drop-protection-firewall.html)
    * [MacOS - source](https://www.privacyaffairs.com/vpn-killswitch/)
    * [What is a VPN Killswitch and how to create one on any device?](https://www.privacyaffairs.com/vpn-killswitch/)
        * [macos - How to auto connect to VPN upon login/boot? - Ask Different](https://apple.stackexchange.com/questions/32392/how-to-auto-connect-to-vpn-upon-login-boot/32395#32395)
        * [Connect to a VPN from the Command Line on Mac OS | by Andreas Siegel | Mac O’Clock | Medium](https://medium.com/macoclock/connect-to-a-vpn-from-the-command-line-on-mac-os-b96f427dbcff)
        * same as above [Connect to a VPN from the Command Line on Mac OS - DEV Community](https://dev.to/andreassiegel/connect-to-a-vpn-from-the-command-line-on-mac-os-1e26)

install ufw

`sudo ifconfig | grep tun0` connect to your VPN and ensure you are connected to tun0
    * same can be done in script  
    ```
    if [[ `sudo ifconfig | grep tun0` ]]; then echo yes; else echo no; fi;
    ```

run the following script, which resets your firewall rules and changes them to only allow tun0.

[vpnkillswitch.sh](../../../../scripts/vpnkillswitch.sh)

## Manual Tasks

[GNU/Linux UFW VPN kill switch tutorial · GitHub](https://gist.github.com/Necklaces/18b68e80bf929ef99312b2d90d0cded2)

[How to make a VPN kill switch in Linux with UFW - Comparitech](https://www.comparitech.com/blog/vpn-privacy/how-to-make-a-vpn-kill-switch-in-linux-with-ufw/)
[Change your macOS power settings to prevent disconnecting from VPN/Wi-Fi when the computer is locked - TechRepublic](https://www-techrepublic-com.cdn.ampproject.org/c/s/www.techrepublic.com/google-amp/article/change-your-macos-power-settings-to-prevent-disconnecting-from-vpnwi-fi-when-the-computer-is-locked/)

* Get info:
    * public IP of the VPN server
    * port and protocol for use with VPN service
    * subnet of your local network
* disable IPv6 in OS and ufw
    * [VPN-How To Connect Successfully & Securely -UFW/OpenVPN/UbuntuMATE 15.04 - Tips, Tricks and Tutorials / Tutorials & Guides - Ubuntu MATE Community](https://ubuntu-mate.community/t/vpn-how-to-connect-successfully-securely-ufw-openvpn-ubuntumate-15-04/1452)
* run VPN as a service (automatic on startup)

### Disable IPv6

Disable IPv6 in ufw config file `/etc/default/ufw` by setting `IPv6=no`.

THen the vpnkillswitch.sh script will also see if the system has it enabled, and if yes, it will disable it.
