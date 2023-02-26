# Contents

- [Change password](#Change password)

:kali:


# Boot options

Buttons to try: F1, F2, F10, F12, Enter, Delete, Escape, Ctrl + Alt Del, Ctrl + Alt + Escape

Ensure in BIOS secure boot is disabled.

# Change password

[source](https://www.youtube.com/watch?v=PxF0E1t3Wts)

## Win 10:
    * `chntpw --help`
    * `chntpw -l SAM` list users (the SAM file is in Windows/System32/config/SAM)
    * `chntpw -u <user>` edit user
        - if this doesn't work, justt use `chtpw -i SAM` interactive mode
    * `0` blank the password
    * `q` quit

Troubleshooting:
    * no windows mounted
        - fdisk -l
        - mkdir windrive
        - mount /dev/sda5 windrive
        - cd to the SAM location
    * SAM file is read only:
        * [How to fix OpenHive(SAM) failed:Read only file system and how to hack pc password using kali linux - YouTube](https://www.youtube.com/watch?v=liSuni9vNio)
        - reboot into windows
        - attemt login with wrong password
        - reboot into Kali
        - continue as normal
