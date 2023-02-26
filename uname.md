UNAME
:uname:

`uname -a` output all OS info
    `-r` release
    `-v` kernel version
    `-n` or `-nodename` network hostname
    `-m` hardware architecture
    `-p` processor type
    `-i` hardware platform
    `-o` OS

Other ways to find out release info:
    `cat /etc/redhat-release`
    `cat /etc/*rel*`
    `dmidecode`


:hostname:
Remember, if you are told to reboot the machine, always type:
`hostname` to ensure it's the correct machine :D
