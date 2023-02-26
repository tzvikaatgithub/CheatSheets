### AWK
:awk:

Visit the [awk & sed tutorial](http://www.theunixschool.com/p/awk-sed.html)

[awk tutorial](https://www.grymoire.com/Unix/Awk.html)

[awk one liners](https://linoxide.com/linux-command/useful-awk-one-liners-to-keep-handy/)

`awk` is a programming language of its own, designed to process text.

[reference](https://www.grymoire.com/Unix/Awk.html)

  `-f` read the awk program from a file. When file is provided, awk reads it line by line

  `{}` holds the code to execute

  `-F "<separator>"` define field separator (default is space). use `'<sep>'` if the separator is a special char, to avoid shell expansion

by default fields are separated by a space

`$0` refers to the entire line

`$1` the first field

`$2` the second field, etc

`~` like operator can be used instead of `==`, where the field contains more than just the string you are comparing to

`awk '$2 == "Jones" {print $0}' awkusers.txt` find lines in file where second field == Jones

`awk '/Jones/ {print $0}' awkusers.txt` using regular expression, this will match "Jonestown"

`awk -F "," '$3 == "Network" {print $1}' warranty.sales.sql.csv | paste -sd+ - | bc` calculate amount of sales for Network devices

`awk -F '|' '$1 ~ /smiths/ {sum += $3} END {print sum}' inputfilename` sum using awk, only sum the 3rd field if 1st field matches a regex

`awk '$4 ~ "12/Nov/2017" {print $0}' access.log` print the line where 4th field is like 12/Nov/2017 (4th field contains both date and time, thus `~` like, is needed)

# AWK Examples


format file1 that has variables var=value to a CSV with proper "","" delimiters
`awk -F"=" '{print "\"" $1 "\",\"" $2 "\""}' file1.txt > file2.csv`
print 3rd column with a comma as the field separator and grep for a value
`awk -F"," '{print $3}' recell-assurant-reporting-1.ca6kirrmxzop.us-east-1.rds.amazonaws.comJune | grep 'QA' | wc -l`
print only the IMEI column
`awk -F ","  '{print $5}' Regans-QA-Data-pulled-from-Engineering-Portal.csv | wc -l`
count 15 digit IMEIs from Assurant file
`awk -F ","  '{print $5}' Regans-QA-Data-pulled-from-Engineering-Portal.csv | grep -E ^[[:digit:]]{15}$ | wc -l`
count uniques
`awk -F ","  '{print $5}' Regans-QA-Data-pulled-from-Engineering-Portal.csv | sed 's/"//g' | grep -E ^[[:digit:]]{15}$ | sort -u | wc -l`
count 15 digit IMEIs in billing (stripping quotes) from OUR billing CSV
`awk -F ","  '{print $1}' billingItems.csv | sed 's/"//g' | grep -E ^[[:digit:]]{15}$ | wc -l`
count 15 digit IMEIs in OUR process Runs CSV
`awk -F ","  '{print $7}' processRuns_0003178.csv | sed 's/"//g' | grep -E ^[[:digit:]]{15}$ | wc -l`

# Parse XML file 
extract value of name="value" inside the first tag
`grep -e '<string' Tests-FR-Strings.xml.md  | awk -F'"' '{ print $2}' > test1.txt`
extract value between tags
`awk -F">" '{print $2 }' myfile.xml | awk -F"<" '{print $1 }' > test2.txt`
combine 2 resulting files into .csv with delimiter
`paste test1.txt test2.txt -d "\n" > results.csv`
