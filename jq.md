JQ
:jq:json:

[intro to JQ](https://sequoia.makes.software/parsing-json-at-the-cli-a-practical-introduction-to-jq-and-more/)

[more info on JQ](https://stedolan.github.io/jq/)

`jq -r '.[] | .[] | .Name, .Type' records.json`

the first .[] gets the first array, the second one gets what is inside and then you get the value you want

## Processing JSON

JSON == JavaScript Object Notation [more JSON info](https://www.json.org/json-en.html)

Objects begin with `{` and end with `}`

name/value pairs can contain values of String, Number, Array, Boolean, or Null

Arrays begin with `[` and end with `]`

`grep -o '"myKey": ".*"' myfile.json | cut -d " " -f2 | tr -d '\"'` extract key/value, then display only the value

`-o` extract only the match, not the whole line

`cut -d " "` delimiter of fields is space

`-f2` extract second field

`tr -d '\"'` remove double quotes

### JQ for JSON Files

`jq` is a lightweight language and JSON parser. Not installed by default on most Linux distros.

[selecting particular pieces of a JSON file, pretty-printing output and filtering data](https://codefaster.substack.com/p/mastering-jq-part-1-59c)

`jq '.title' myfile.json`

`jq '.authors[].firstName' myfile.json` list *all* values of an array `authors[]`, or use `[n]` for specific ones
