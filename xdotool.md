:xdotool:

[xdotool - fake keyboard/mouse input, window management, and more - semicomplete](https://www.semicomplete.com/projects/xdotool/)

Basic usage is: `xdotool <cmd> [args]`.

Focus on FireFox URL bar:
`xdotool search "Mozilla Firefox" windowactivate --sync key --clearmodifiers ctrl+l`

Resize all visible gnome-terminal windows:
```
xdotool search --onlyvisible --classname "gnome-terminal" windowsize %@ 500
```

Select window with mouse to kill it
`xdotool selectwindow windowkill`
