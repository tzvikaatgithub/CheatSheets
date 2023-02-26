:user:management:
:adduser:useradd:usermod:userdel:deluser:
:passwd:
:chsh:

# Create User

You'll need root permissions.

Remember, you can do it in GUI too :) you might need `gnome-system-tools` package. While some distros have it built in (User Manager in KDE).

Interactively:
    * `adduser <username>`

Manually:
    * `useradd -m <username>` add home dir. You'd need to add him to Group if you want to give him sudo access

# Set Password

`passwd <username>`

# Group Management

`usermod -a -G sudo <anotherGroup>`
    `-a` add user
    `-G` specify group(s)

`sudo usermod -G sudo <user>` make user sudoer

# Change Shell

`chsh -s /bin/bash <username>` set or change shell of the user

# Delete User

This is a low level utility:

`userdel <username>` just remove the user

delete the user's home dir and mail spool

`userdel* <username>`

`userdel -r* <username>`

If the user is currently logged in, you need to either killall user first, or provide -f switch to userdel

`sudo killall -u <username>`

`sudo userdel -f <username>`

Debian admins usually use `deluser` instead
