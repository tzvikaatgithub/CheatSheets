## Processing XML

`grep -Pzo '(?s)<myTag>.*?<\/myTag>' myfile.xml | sed 's/<[^>]*>//g'` extract data contained between the myTag tag found on multiple lines, and strip the XML tags

`-o` return only the value matching the regex between the `''` pattern, not the whole line

`-P` specifies Perl-specific pattern match modifier, allowing the use of `(?s)`, which modifies the `.` metachar to also match on the newline char (not avail on MacOSX, and not on all versions of grep)

`-z` treat newlines like ordinary chars and add a null value (ASCII 0) at the end of each string it finds

Reminder, here is what a sed expression means: `sed 's/<expr-to-replace>/<replace-with>/g'`

`<` in our case we start with a literal <

`[^>]*` here `*` means zero or more of chars inside `[]`, and `^>` means not >, thus matching a single XML tag

