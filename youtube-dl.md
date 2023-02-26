youtube-dl
:youtube-dl:

Official remaining repo [youtube-dl](https://yt-dl.org/download.html)

[youtube-dl - ArchWiki](https://wiki.archlinux.org/title/Youtube-dl)

# Installation

Manual [Installtion](https://github.com/ytdl-org/youtube-dl/blob/master/README.md#how-do-i-update-youtube-dl)
```
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```

`youtube-dl -x --audio-format mp3 <vid-URL>` download video and convert to mp3

# Find best format to download

`youtube-dl -F <url>` lists numbers and formats next to each other

`youtube-dl -f <nb> <url>` your chosen format

MP4 and M4A specifically:

`youtube-dl -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/mp4' <url>`

# Format selection examples

This is from the man page

Note that on Windows you may need to use double quotes instead of single.

   Download best mp4 format available or any other best if no mp4 available
   `youtube-dl -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best'`

   Download best format available but no better than 480p
   `youtube-dl -f 'bestvideo[height<=480]+bestaudio/best[height<=480]'`

   Download best video only format but no bigger than 50 MB
   `youtube-dl -f 'best[filesize<50M]'`

   Download best format available via direct link over HTTP/HTTPS protocol
   `youtube-dl -f '(bestvideo+bestaudio/best)[protocol^=http]'`

   Download the best video format and the best audio format without merging them
   `youtube-dl -f 'bestvideo,bestaudio' -o '%(title)s.f%(format_id)s.%(ext)s'`

Note that in the last example, an output template is recommended as bestvideo and  bestaudio may have the same file name.

Setting destination file is possible using the `-o` switch, again - this is a file, not dir. But you can also cd into the dir and download or download first and then move where you want it.
