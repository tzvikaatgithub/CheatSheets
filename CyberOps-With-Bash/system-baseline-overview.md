Malware infections and other intrusions can often be detected by the changes they make to the filesystem of a target. You can use the properties of a cryptographic hash function and a little command-line wizardry to identify files that have been added, deleted, or changed over time. This technique is most effective on systems such as servers or embedded devices that do not change significantly on a regular basis.

Steps:
    1. record the path of every file on a given system
    2. create SHA-1 hash of every file on it
    3. re-run the tool at a later time and output any files that have been changed, deleted, moved or new

For best results a system should be baselined when it is in the state of known-good configuration.
