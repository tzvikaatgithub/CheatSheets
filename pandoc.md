PANDOC
:pandoc:

Pandoc is a cli tool for converting between the different file formats

To convert a valid markdown doc to a text file
`pandoc -f markdown -t plain Git-Workflow-Feature-Branch.md > FeatureBranch.txt`
`-f` is a format to convert from
`-t` is a format to convert to
then comes the name of the source file and we redirect it to an output file

To convert a valid markdown doc to a pdf
`pandoc --variable urlcolor=cyan -f markdown -o text.pdf text.markdown | opdf text.pdf`
To convert a valid markdown doc to a html
`pandoc --variable urlcolor=cyan -f markdown -t html5 -o myfile.html myfile.md; firefox myfile.html &`

To pipe Sefaria .txt through a pager
`pandoc -f html -t plain /absolute/path/file.txt | rev | less`
the only issue is that Hebrew text is written right to left inside the file,
we are using rev to reverse them.
there is also a `column -t` command to align the text, but i couldn't get it to work as i wish
