FDISK
:fdisk:

[source](https://www.tecmint.com/fdisk-commands-to-manage-linux-disk-partitions/)

View all partitions
`fdisk -l`

View specific disk partition
`fdisk -l /dev/sda`

Check all available commands
`fdisk /dev/sda`
after the fdisk prompt starts, enter `m`

Print partition table
`fdisk /dev/sda`
after the fdisk prompt starts, enter `p`

Delete partition
`fdisk /dev/sda`
after the fdisk prompt starts, enter:
    1. `d`
    2. partition number
    3. `w`

Create New (extended) partition
`fdisk /dev/sda`
after the fdisk prompt starts, enter:
    1. `n`
    2. `e`
    3. size (first and last cylinder). ex: `+5000M`
    4. `w`

Format new partition
`mkfs.ext4 /dev/sda4`

Check size of partition
`fdisk -s /dev/sda4`

see more at the source about fixing partition out of order error and disabling boot * flag
