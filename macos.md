:macos:

# Create ISO

[Create A macOS Monterey Installer ISO - For VirtualBox Running On Windows - YouTube](https://www.youtube.com/watch?v=q9koLQSqrlc)

Command #1: hdiutil create -o /tmp/Monterey -size 16384m -volname Monterey -layout SPUD -fs HFS+J

Command #2: hdiutil attach /tmp/Monterey.dmg -noverify -mountpoint /Volumes/Monterey

Command #3: sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/Monterey --nointeraction

Command #4: hdiutil eject -force /Volumes/Install\ macOS\ Monterey

Command #5: hdiutil convert /tmp/Monterey.dmg -format UDTO -o ~/Desktop/Monterey

Command #6: mv -v ~/Desktop/Monterey.cdr ~/Desktop/Monterey.iso

Command #7: rm -fv /tmp/Monterey.dmg
