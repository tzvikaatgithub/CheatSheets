# Commands in All Wikies
:vimwiki:

`<Leader>ws` - list all available wikies

## List Commands

`:h vimwiki-commands` -- list all vimwiki commands

## Key Bindings

`:h vimwiki-mappings` - *All* VimWiki Key Bindings
`<Leader>ww` -- Open default wiki index file. My personal shortcut for "save" overrides this.
`<Leader>wt`-- Open default wiki index file in a new tab.
`<Leader>ws` -- Select and open wiki index file.
`<Leader>wd` -- Delete wiki file you are in.
`<Leader>wr` -- Rename wiki file you are in.
`<Enter>` -- Follow/Create wiki link
`<Shift-Enter>` -- Split and follow/create wiki link
`<Ctrl-Enter>` -- Vertical split and follow/create wiki link
`<Backspace>` -- Go back to parent(previous) wiki link
`<Tab>` -- Find next wiki link
`<Shift-Tab>` -- Find previous wiki link

## Title Example

---
title: My Personal Wiki!
subtitle: >
This is a collection of things that I know,
things that I learn,
and things that I want to remember.
---

## Table of Contents
:toc:

`:VimwikiTOC` inserts table of contents at the beginning of the file; if exists - it updates it.

