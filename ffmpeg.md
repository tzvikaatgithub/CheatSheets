FFMPEG
:ffmpeg:

# Contents

- [Intro](#Intro)
- [Extract Audio from Video](#Extract Audio from Video)
- [Misc](#Misc)

# Intro

ffmpeg is a video and audio converter

[Official docs](https://ffmpeg.org/ffmpeg.html)

# Extract Audio from Video

[source](https://www.linuxuprising.com/2019/11/ffmpeg-extract-audio-from-video-in.html)

`ffprobe myfile` find data type of your file (look for the line which starts with 'Stream')

`ffmpeg -i myfile -vn -acodec copy audio.ogg` extract audio without re-encoding
    * `-i` is used to specify the path and filename of the input video
    * `-vn` skips the inclusion of the video stream
    * `-acodec copy` is for copying the original audio (without re-encoding).
    * `-ss 00:00:00 -t 00:00:00.0` extract a portion from `-ss` start `-t` for duration



# Misc

`ffmpeg -fflags +genpts -i ~/myfile.webm -r 24 output-file.mp4` Convert from .webm to .mp4


