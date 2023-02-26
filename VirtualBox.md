VIRTUALBOX

:virtualbox:

# Contents

- [Host, NAT, Bridged](#Host, NAT, Bridged)
- [Downloads](#Downloads)
- [Installation](#Installation)

# Host, NAT, Bridged
[source](https://superuser.com/questions/227505/what-is-the-difference-between-nat-bridged-host-only-networking#227508)
    * Host-only only permits network operations between the Guest VM and the Host OS.
    * NAT mode will mask all network activity as if it came from your Host OS, although the VM can access external resources.
    * Bridged mode replicates another node on the physical network and your VM will receive it's own IP address if DHCP is enabled in the network. It allows comms between the Host OS and the VM, plus it allows comms with the internet.

# Downloads

[Get Kali | Kali Linux](https://www.kali.org/get-kali/#kali-virtual-machines)

# Installation

* [Linux_Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Linux_Downloads)
* [Kali inside VirtualBox (Guest VM) | Kali Linux Documentation](https://www.kali.org/docs/virtualization/install-virtualbox-guest-vm/)

# Metasploitable 2 on VirtualBox
:metasploitable:
https://linuxhint.com/metasploitable_training_environment_virtualbox/
default user and password: `msfadmin`
