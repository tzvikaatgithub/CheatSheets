SPLIT
:split:

[source](https://linoxide.com/linux-how-to/split-large-text-file-smaller-files-linux/)

Split the file, based upon the number of lines (500 in this case)
`split -l 500 filename`

`-a –suffix-length=N` use suffixes of length N (default 2)
`-b –bytes=SIZE` put SIZE bytes per output file
`-C –line-bytes=SIZE` put at most SIZE bytes of lines per output file
`-d –numeric-suffixes` use numeric suffixes instead of alphabetic
`-l –lines=NUMBER` put NUMBER lines per output file

Split gives each output file it creates the name prefix ('x' by default) with an extension ('aa' and goes through alphabet by default) tacked to the end that indicates its order.

if prefix contains a dir pattern, it will put the file in the target dir.

`split -l 500 filename prefix`
