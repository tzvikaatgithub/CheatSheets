### SED
:sed:

Visit the [awk & sed tutorial](http://www.theunixschool.com/p/awk-sed.html)

`sed` allows to perform edits on a stream of data. Ex: replacing chars

`-i` edit specified file and overwrite in place

`sed 's/<regex>/<replace-with>/<flags>' <file>`

`s` substitute

inside regex you need to use `\` to escape special chars

`g` global substitution - eg. everywhere on the line, not just the first match

Separate the openvpn keys from .ovpn file:

    `sed '1,/<ca>/d;/\/ca>/,$d' john.ovpn > ca.crt`

    `sed '1,/<cert>/d;/\/cert>/,$d' john.ovpn > client.crt`

    `sed '1,/<key>/d;/\/key>/,$d' john.ovpn > client.key`

    `sed '1,/<tls-auth>/d;/\/tls-auth>/,$d' john.ovpn > ta.key`
