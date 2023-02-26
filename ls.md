LS

:ls:

`ls -ltr` reverse long list: newest at the top, oldest at the bottom

List only dirs:
`ls -d */` List only dirs
    `-F` append trailing slash to dirs; with this you can `|grep \/$`
    `ls -l | grep ^d` in the long listing grep for whatever starts with d

`ls`
    `-B` omit backup files, those ending with a tilde

Output formatting:
    `ls -X` or `--` output in columns
    `-1` one per row

Sort:
    `ls` default is by name equivalent of `ls --sort=none`
    `-S` or `--sort=size` sort by size
    `-U` or `ls --sort=time` sort by when it was accessed
    `-r` reverse the sort order
