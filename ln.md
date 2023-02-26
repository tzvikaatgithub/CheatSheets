### LN
:ln:
- inode number is like an ID of the file on Linux system
- ln -s [target-file] [symlink-file]. Soft link, symlink (symbolic link) is like a shortcut. Target file and symlink file have different inode numbers (ls -i).
- ln [target-file] [hard-link]. Hard link is an additional name for the same file. Hard link has the same inode number

Create symlink
`ln -s /path/to/source/dir/ /path/to/symlink`
relative symlink
`ln -rs ../rel/path/to/source/dir/ [./path/to/destination/]symlink`

`ln [options] -T <target> <link_name>` treat link name as a normal file, as opposed to `-t <dir> <target>` which specifies a dir in which links are created

Find real path of a file
`realpath myfile.sh`

Set alarm/timer to play music
`sleep 20m && rhythmbox myfile.mp3`

