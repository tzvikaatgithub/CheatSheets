SQLite
:sqlite:

# Contents

    - [Resources](#Resources)
    - [CheatSheets](#CheatSheets)
    - [Import CSV into SQLite DB](#Import CSV into SQLite DB)
    - [Commands Examples](#Commands Examples)

## Resources

* Great [tutorial](https://www.sqlitetutorial.net/) and each statement referenced on right
    * common commands explained https://www.sqlitetutorial.net/sqlite-commands/
* Knowledge Base ideas: https://github.com/gnebbia/kb/
* Difference between SQL and SQLite https://www.sqlite.org/lang.html
* SQLite cli client with completion and syntax highlighting https://litecli.com/


## CheatSheets

* https://cheatography.com/explore/search/?q=sqlite
* https://www.sqlitetutorial.net/sqlite-cheat-sheet/

## Import CSV into SQLite DB

CSV to SQLite [tutorial](https://www.sqlitetutorial.net/sqlite-import-csv/)
Connect from cli:
`sqlite3 example.db`
sqlite> .mode csv
sqlite> .import <your-file.csv> <your-table-name>
sqlite> .exit


## Commands Examples

sqlite> .tables
sqlite> .schema table
sqlite> .help
sqlite> .quit
sqlite> .system ls -l
