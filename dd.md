DD
:dd:
dd - convert and copy a file.

# Contents

- [Intro](#Intro)
- [Basics](#Basics)
- [Wiping Disks](#Wiping Disks)
- [Monitoring dd Operations](#Monitoring dd Operations)

# Intro

[source](https://opensource.com/article/18/7/how-use-dd-linux)

dd is great for working on partitions.

D.D. == disk destroyer. If you mistype even one char you can permanently wipe out an entire drive of data.

While tar and scp will allow you to copy an entire filesystem, it will still require an OS on both ends. Instead, dd creates an image, a perfect copy byte for byte.

Create a USB bootable drive from iso using a single terminal command:
`dd if=/home/user/Downloads/ubuntu.iso of=/dev/sdb1 bs=512M; sync`
The command above creates a USB drive (/dev/sdb1) into a Debian bootable drive.

# Basics

Create an exact image of an entire disk:
`dd if=/dev/sda of=/dev/sdb`
    `if` input file, the sourcce
    `of` output file, the destination, it can be a file or a disk

Create an .img archive of an entire /dev/sda drive
`dd if=/dev/sda of=/home/username/sdadisk.img`

Create an .img archive of the /dev/sda2 partition
`dd if=/dev/sda2 of=/home/username/partition2.img bs=4096`
    * `bs` byte size that is copied in a single time, this affects speed of the operation
    * bs - block size, the default is 512B, which is an old standard, we can set it to a more modern setting of 64K

Resotre by reversing if and of
`dd if=sdadisk.img of=/dev/sdb`

Create a compressed image of a remote drive using SSH and save the resulting archive to your local machine:
`ssh username@54.98.132.10 "dd if=/dev/sda | gzip -1 -" | dd of=backup.gz`

Always TEST YOUR ARCHIVES to confirm they are working.

# Errors and Progress


`dd if=/dev/sda of=/dev/sdb bs=64K conv=noerror,sync status=progress`
    * conv - noerror means dd will continue ops even if it hits an error, this is not the default
    * sync will fill input blocks with zeros, so the data offset will stay in sync
    * status will allow you to monitor the progress

# Wiping Disks

## HDD

dd doesn't really erase anything, at least on SSD, it just marks it as erased.

Write millions and millions of zeros over every nook and cranny of the /dev/sda1 partition:
`dd if=/dev/zero of=/dev/sda1`

Write over a disk with random characters:
`dd if=/dev/urandom of=/dev/sda1`

# Monitoring dd Operations

Disk or partition archiving can take a very long time.

Add a progress monitor to dd:
`dd if=/dev/urandom | pv | dd of=/dev/sda1`
    You will need to install pv

## SSD

[Securely Erasing Your SSD with Linux: A How-To – Techgage](https://techgage.com/article/securely-erasing-your-ssd-with-linux-a-how-to/)

Useful commands (which require root (su) or sudo (sudo -s, or just type “sudo” before each command):

    hdparm -I /dev/sdX – Displays all information about a drive.
    hdparm -I /dev/sdX | grep Model – Displays the drive brand and model.
    hdparm -I /dev/sdX | grep frozen – Displays whether or not the drive is frozen (“not” is required).
    hdparm –security-erase PASS /dev/sdX – Simple command to secure erase a drive with no hassle.
If it throws an error, use the commands below:
    hdparm –user-master u –security-set-pass /dev/sdX – Sets a password.
    hdparm –user-master u –security-erase /dev/sdX – Securely erases the SSD.
    

Note: There are two dashes before the user-master and security- commands. The info commands above use a capital i, not a small L.

An important command here is either the first or third. We need the drive to be “not” frozen, and if that’s the case, then it’s a matter of running the fourth command

[Solid state drive/Memory cell clearing - ArchWiki](https://wiki.archlinux.org/title/Solid_state_drive/Memory_cell_clearing)
