:hardware:commands:

GUIs:
:hardinfo:
`hardinfo`

:sysinfo:
`sysinfo`
Sysinfo is a graphical utility that is able to gather some software and hardware information about the system. It is able to display information about:
    * System (Linux distribution release, kernel, gcc, versions of GNOME , Xorg and hostname)
    * CPU ( model name,vendor identification, frequency, bogomips,level2 cache, model numbers , flags…)
    * Memory ( RAM, free memory, total and free swap space, active, inactive and cached memory)
    * Storage (IDE interface, SCSI devices, all IDE devices)
    * Hardware ( graphic card, motherboard, sound card and network devices)
    * NVIDIA graphic card: In case NVIDIA display driver is installed

:dmidecode:

cli tool.

`dmidecode` (Desktop Management Interface table decoder), retrieves data from DMI table ( also known as SMBIOS) and produces it in a human readable format.

It displays Ubuntu hardware info such as BIOS details, Processor, RAM(DIMMs), Memory, BIOS detail, Serial numbers etc

`sudo dmidecode -t system` (UUID) motherboard serial number

`sudo dmidecode -t baseboard`

`sudo dmidecode -t bios`

:lsblk:

lsblk - List information about block devices.
`lsblk --all` list all of them

:lshw:
lshw stands for list hardware. It generates detailed information about various hardware devices present on the system by reading the /proc filesystem.

It also has gui: lshw-gtk

Use root.

`lshw` full information report about all detected hardware.

`lshw -short` will produce brief information

`sudo lshw -short -class memory` only memory info

`sudo lshw -class processor` CPU info. Note: number of cores might be off.

`sudo lshw -short -class disk` disk drives
`sudo lshw -short -class disk -class storage -class volume` with partitions and controllers

`df -h` display system partition with size

`sudo lshw -class network` network adapter. Serial is the Mac

`sudo lshw -businfo` address details of pci, usb, scsi and ide devices

Generate report:
    `sudo lshw -html > hardware.html`
    `sudo lshw -xml > hardware.xml`

:lspci:

`lspci` Displays information about the PCI buses in the system and devices connected to them.

`lspci -vvv` verbose output contains the name of the driver for that PCI device

`lspci -tree` in a tree format

Examples:
    `lspci -nnk | grep VGA -A1` info about graphics
    `lspci -v | grep -A7 -i "audio"` info about audio
    `lspci -nnk | grep net -A2` networking

:lspcu:

`lscpu` Displays information on CPU Architecture

:lsusb:

`lsusb` - List all usb devices

:lsdev:

`lsdev` - Displays information about installed hardware by gathering information from interrupts, ioports, and dma files in the /proc directory.

This command is not present by default, you need to install it by running "sudo apt-get install procinfo

:hardware:monitoring:commands:

[source](https://net2.com/ubuntu-debian-monitoring-tools-guide-for-system-administrators/)

:attached:hardware:
:udev:dmesg:

Udev listens to events from the Linux kernel involving changes to the state of a device (plugged/unplugged).

It then handles all changes of state. It assigns the names or permissions through which devices are accessed.

Dmesg lists records of those changes.

On systemd a daemon called systemd-udevd manages udev ops.

`systemctl status systemd-udevd`

Udev tries to match system events against sets of Rules in `/lib/udev/rules.d/` or `/etc/udev/rules.d/`

Match keys include `action`, `name`, and `subsystem`. If name and subsystem match a device, action is applied to it.
