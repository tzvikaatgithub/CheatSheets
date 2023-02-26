FIREFOX
:firefox:

# Contents

- [Tips](#Tips)
    - [Profiles](#Tips#Profiles)
- [HTTPS Only Mode](#HTTPS Only Mode)
- [MacOS](#MacOS)
    - [Navigation](#MacOS#Navigation)
    - [Tabs](#MacOS#Tabs)
    - [Files](#MacOS#Files)
    - [Misc](#MacOS#Misc)
    - [Search](#MacOS#Search)

# Tips

open last tab
`<C-S-t>`

`open -a Firefox 'http://www.youtube.com/'` open firefox in Macos

firejail is for sandboxing firefox on linux.

[Keyboard shortcuts](https://support.mozilla.org/en-US/kb/keyboard-shortcuts-perform-firefox-tasks-quickly)

## Profiles

files are located in ~/.mozilla/

[Firefox help docs](https://support.mozilla.org/en-US/kb/profiles-where-firefox-stores-user-data)

[Best FireFox Hardening Resource](https://github.com/pyllyukko/user.js)
    * drop user.js file into your firefox dir
    * make a test profile to test this

`firefox -P` open a specific profile
    profiles are used for different configs
    you can test plugins/addons in profiles without messing up the rest

# HTTPS Only Mode

    1. Click on Firefox’s menu button and choose “Preferences”.
    2. Select “Privacy & Security” and scroll down to the section “HTTPS-Only Mode”.
    3. Choose “Enable HTTPS-Only Mode in all windows”.


There are a bunch of 'about' protocols, check this list: [The about protocol](https://developer.mozilla.org/en-US/Firefox/The_about_protocol)

about:profiles
    Profiles

about:support
    Troubleshooting information about your FireFox app

about:plugins
    installed plugins

about:network
    tells you about current connections

about:cache
    shows what's in memory, on disk

about:memory
    tells you about

about:config
    * low level settings, such as not sending HHTP Referrer
    * more info: http://kb.mozillazine.org/About:config
    * breakdown of entries that you can find and change: http://kb.mozillazine.org/Firefox_:_About:config_Entries with descriptions
    * Firefox Security and privacy related preferences http://kb.mozillazine.org/Category:Security_and_privacy-related_preferences
    * most hardening is done here
    * accept "be careful"
    * search for `Network.http.sendReferrerHeader`, edit and set to 0 (instead of 2)
        * this won't send referrer to the website
    * search for `browser.urlbar.trimURLs` and change to `false`
        * this makes a clear indicator in URL if it's HTTP or HTTPS
    * search for `security.ssl3`
        * allows you to switch which security suite you use.
        * there is an addon Cipher Suites that lets you do it in a gui
    * `browser.sessionstore.resume_from_crash` true/false - set default true to false, so sessions do not restore on next start

# MacOS

[Firefox (macOS) keyboard shortcuts ‒ defkey](https://defkey.com/firefox-mac-shortcuts)

## Navigation

`Cmd ]` forward To next page

`Cmd [` back To previous page

`Tab` focus on next link or input

`Space` go down a screen

`Shift Space` go up a screen

`Cmd arrow down` go to bottom

`Cmd arrow up` go to top

## Tabs

`Cmd W` close tab

`Cmd Shift T` undo close tab

`Ctrl Tab` cycle through tabs

`Cmd Opt arrow left` go to tab on left

`Cmd Opt arrow right` go to tab on right

`Cmd T` new tab

`Cmd W` quit tab


## Files

`Cmd O` open file

`Cmd J` show downloads

`Cmd P` print

## Search

`Cmd K` focus on search bar

## Misc

`Cmd R` reload

`Cmd Shif R` reload and override cache

`Cmd +` Zoom in

`Cmd -` Zoom out

`Cmd Q` quit window

`Cmd N` new window

`Cmd D` bookmark this page

`Cmd Shift B` toggle bookmarks toolbar
