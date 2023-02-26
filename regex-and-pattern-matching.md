# Pattern Matching (not regex)
:bash:pattern:

patterns are matched against the current dir. if you begin it with a path, the pattern will be matched against that dir.

no pattern matching occurrs inside double quotes, the special pattern matching chars will be taken literally. ex: `echo data > /my/path/*.out` will create a file called *.out

if no match had been made, the pattern mathing chars will be used literally. `echo data > *.out` if there is no file with extention .out, a file called *.out will be created

wildcard:
`*` matches all files in the dir
`?` matches one char
`[ ]` matches any one of the chars listed inside the swuare brackets. ex: `x[abc]y.pdf` will match xay.pdf, xby.pdf and xcy.pdf

ranges:
`[0-9]` will match any digit
`[!0-9]` or `[^0-9]` negates anything matched by square brackets. ex: `[^aeoiu]` matches consonants, digits and punctuation chars (eg. non-vowels)

Classes
`[:alnum:]` alphanumeric
`[:alpha:]` alphabetic
`[:ascii:]` ASCII
`[:blank:]` space and tab
`[:ctrl:]` control chars
`[:digit:]` numbers
`[:graph:]` anythung other than control chars and space
`[:lower:]` lower case chars
`[:print:]` anyhing other than control chars
`[:punct:]` punctuation
`[:space:]` whitespace incl. line breaks
`[:upper:]` uppercase
`[:word:]` letters, numbers, and underscore
`[:xdigit:]` hexadecimal
Classes are used inside a second pair of square brackets. ex: `*[[:punct:]]jpg` will match lala!jpg and bahbah,jpg

advanced pattern matching can be turned on
`shopt -s extglob`
learn more about it in `man bash`. things like repeating or negating patterns

# Regex
:bash:regex:

Regular Expressions are valid in *Bash* ONLY inside the `[[` compound command, using the `=~` comparison.

However, regular expressions are a crucial part of the larger toolking for commands like `grep`, `awk`, and `sed` in particular.

## Resources

http://www.rexegg.com/

https://regex101.com

https://www.regextester.com/

http://www.regular-expressions.info/


### Extended Syntax for Regex Patterns

The standard regex is created using chars and metacharacters. Metacharacters require `-E` flag.

To treat a metacharacter as a literal character, you must escape it.

Regex patterns are case sensitive.

If you were to run `grep` and wanted to use them as metacharacters, you would need to escape them.

Regex metacharacters: `^ $ . [ ] { } - ? * + ( ) | \`, they must me enclosed in quotes to prevent the shell expansion

The `^ $ . [ ] *` are basic regular expression metachars. In BRE, metachars `( ) { }` escaped with `\` are considered metachars

Extended regular expressions support `? + { } | ( )` metachars. In ERE Metachars `( ) { }` escaped with `\` are treated as literals.

All other chars are considered literals.

#### Regex Metacharacters:

`.` single wildcard char, except for a newline. Obviously, it has to be at least one char.

`?` any item that precedes it zero or one time is optional.

`*` any item that precedes it zero or more times.

`+` any item that precedes it one or more times.

#### Grouping

Parentheses `( )` are used to group chars. The expression inside the parentheses is treated as one item

Groups can be remembered for later.

Here is how to match either OR using the `|` boolean OR:
`egrep 'And be one (stranger|traveler), long I stood' frost.txt`

Brackets `[ ]` are used to define Character Classes and lists of acceptable chars at specific positions. Ex: validate user input.

Metachars lose their special meaning when placed within brackets. Exceptions inside brackets are `^` indicating negation and `-` which indicates a range.

Literals inside brackets are taken as having OR between them.

Shortcuts that are supported only in Perl `grep -P` (not `egrep`; and there is no `grep -P` on Unix):

`\s` Whitespace

`\S` Not whitespace

`\d` digit

`\D` non-digit

`\w` word

`\W` non-word

`\x` hexadecimal number

Regex Character Classes (shortcuts):

`[:alnum:]` Any alphanumeric char

`[:alpha:]` any alphabetic char

`[:cntrl:]` any control char

`[:digit:]` any digit

`[:graph:]` any graphical char

`[:lower:]` any lowercase char

`[:print:]` any printable char

`[:punct:]` any punctuation

`[:space:]` any whitespace

`[:upper:]` any uppercase char

`[:xdigit:]` any hex digit

Note - since char classes must go inside a grouping `[ ]`, you end up with a double bracket set `[[:classname:]]`. Thus if you place two classes inside the first set of brackets (eg. `[[:classA:][:classB:]]`) then these classes will be treated as having `|` OR between them.

Back References can be made to a group (surrounded by `( )`) in the order it appears in the regex:

`egrep '<([A-Za-z]*)>.*</\1>' html-file.html`

here `\1` refers to `[A-Za-z]*`, which appears as the first group. You may have `\2`, `\3` etc.

#### Quantifiers

Quantifiers `{ }` specify the number of times an item must appear in a string.

`T{3,6}` means T must appear 3 to 6 times
`T{3,}` means T must appear 3 or more times

#### Anchors and Word Boundaries

`^` beginning of the string

`$` end of the string

