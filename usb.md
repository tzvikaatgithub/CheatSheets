USB
:usb:types:bootable:

# USB Standards

USB (universal serial bus) - de facto standard by which we plug something into our machine.

USB is backward compatible.

USB Standards:
    * 1.1:
        - 1.5mbps||12mbps 
        - color: white (most likely)
    * 2.0:
        - 480mbps
        - color: black
    * 3.0:
        - 5Gbps
        - had issues
        - color: blue
    * 3.1:
        - gen 1 5Gbps
        - color: blue
    * 3.1:
        - gen 2 10Gbps
        - color: teal
    - Charging ports:
        - specialized ports
        - color: orange, red, yellow

Speeds are super important for the exam.

Physical connectors:
    * A
        - flat A connector
    * B
        - more square one, with 2 flat and 2 sharp corners (similar to printer)
    * mini-B
        - cameras and video recorders
    * micro-B
        - android devices
    * 3.0 micro connector
        - has 2 parts - larger part is like micro-B and a smaller one
        - (micro-B can be plugged in)
    * C
        - very high speeds
        - can be plugged in any way

[USB Type-C Explained: What is USB-C and Why You’ll Want it](https://www.howtogeek.com/211843/usb-type-c-explained-what-it-is-and-why-youll-want-it/)

# Creating Bootable USB

## Software

There are multiple tools which can help you create a bootable USB
    * [Rufus - To create a bootable USB/SD card with the ISO](http://rufus.akeo.ie/)
    * [Pendrive linux](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/)
    * [Tails - Manually installing onto a USB stick or SD card](https://tails.boum.org/install/)
        * [install Tails using cli](https://tails.boum.org/install/expert/usb/index.en.html)

## Cli

If you want to restore an image you basically only need one command:

`sudo lsblk -d | grep disk`

`sudo dd bs=4M if=path-to-the-ISO of=/dev/sdX status=progress && sync`

`sudo dd bs=4M if=path/to/archlinux-version-x86_64.iso of=/dev/sd<X> conv=fsync oflag=direct status=progress`

Do you need formatting it? Need research.

## GUI

Here is an easy guide using built in OS tools:

Creating Debian 10 Bootable USB Thumb Drive for Installing Debian 10 – Linux Hint
https://linuxhint.com/debian_10_bootable_usb_install/

Use GNOME disks, restore image on the USB stick using the .iso you've downloaded
