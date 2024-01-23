# Learning Escape Characters
Escape characters are used when trying to use either single or double inverted commas.  As an example, bash scripting uses " " for literal strings.  If the string that I wanted to add to a variable, the inverted commas are parsed as part of the scripting language syntax rather than the string value.  This issues is managed with 'escape characters', which provides the ability to have these characters as part of the variable.

~~~ bash
#!/bin/bash

# this script creates a variable called 'learningbash' with a value of "Hello World" and then prints the value to the console.

learningbash="Hello World"
echo $learningbash

# in this example, the inverted commas are used to assign a value to the variable however this wont work if you if the variable requires a inverted comma in the variable

learningbash_2="This is a "quote""
echo $learningbash_2

~~~


