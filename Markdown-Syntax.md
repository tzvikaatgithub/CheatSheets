:markdown:

[Neovim editing and preview](https://jdhao.github.io/2019/01/15/markdown_edit_preview_nvim/)
    * [GitHub - iamcco/markdown-preview.nvim: markdown preview plugin for (neo)vim](https://github.com/iamcco/markdown-preview.nvim)

[online resource](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

[command line - Markdown Viewer - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/4140/markdown-viewer#120519)

=== Headers ===

# H1
## H2
### H3
#### H4
##### H5
###### H6

=== Emphasis ===

*bold*
_italic_
**two bold**
__two italic__
There are a few typefaces that give you a bit of control over how your text
is decorated: >

  *bold text*
  _italic text_
  ~~strikeout text~~
  `code (no syntax) text`
  super^script^
  sub,,script,,

Furthermore, there are a number of words which are highlighted extra flashy:
TODO, DONE, STARTED, FIXME, FIXED, XXX.

> hello
>
>>> hello

1. one
2. two
3. three


1. asdf
1. sadf

* asterisk
* another

+ plus
+ plus

- minus
- minus
    - indented

# Images don't work
    ![image](~/screenies/select-os-as-is.png)
# Link
    [link](http://www.example.com)
    [link](http://www.example.com "Link title hoes here")

# URL and Email don't work
<gmogilevsky@assetscience.com>
<http://www.example.com>

# Code
`for i in range(0, 100):`
`    print(i)`

# Horizontal Rules don't work
***
---
___


# Key Mappings
`<Leader>wd` deletes the current wiki page

# Testing
links to websites open in web browser by clicking `<Enter>`
[link to website](https://assetscience.com)
links to files only work if they are executed with `gx` with cursor on full path name
[link to file](/home/george/Documents/wlcome.odt)

