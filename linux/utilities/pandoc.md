# Pandoc
## Introduction
pandoc is used to convert between different types of markup languages.

https://pandoc.org

## Install
~~~ bash

sudo apt install pandoc

~~~

## Syntax
~~~ bash

# convert markdown to html
# -f >> input format
# -t >> target format
# -s >> standalone create output with appropriate headers (html)
# -o >> output file


pandoc markdown_file.md -f markdown -t html -s -o target_file.html



~~~