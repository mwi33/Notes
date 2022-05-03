# Regular Expressions
Regular expressions (regex) is a method for finding patterns in text.

~~~ bash

# strings with spaces need to be with in single or double quotation marks

grep 'gnome display manager' /etc/passwd


~~~

## Anchoring

Anchors are used to specify where in the line the match must be found.

### Beginning of line
The ^ symbol matches the empty string at the beginning of the line.

~~~ bash

# a match only if hello is the first string in the line

grep '^hello' hello_world.txt

# a match only if hello is the last string in the line

~~~

### End of line
The $ symbol matches the empty string at the end of the line.

~~~ bash

# a match only if hello is the last string in the line

grep 'hello$' hello_world.txt

~~~

### Only
Both anchors can be used to match when the string is the only item on the line.

~~~ bash

# a match if it is the only item on the line

grep '^hello$' hello_world.txt

~~~

### Matching a single character

The period (.) can be used to match a single character.

~~~ bash

# use the . as a place holder for any character

grep 'kan..roo' hello_world.txt

~~~

Will return any string that has 'kan' followed by two characters and finally 'roo'.

### Bracket expressions

Bracket expressions allow the matching of multiple characters by enclosing them in brackets.  

~~~ bash

# use a bracket expression to find either 'accept' or accent

grep 'acce[np]t' hello_world.txt

~~~

Using the ^ in brackets will match any character this isnt included.

~~~ bash

# match any work that starts with 'co' and ends in a, however, does not have 'l' in between

grep 'co[^l]a' hello_world.txt

~~~

Instead of specifying each character, a range can be used.  [a-e] is the same as [abcde].

~~~ bash

# This expression will match any line that starts with a capital letter.

grep '^[A-Z]' hello_world.txt

~~~

### Classes
grep all supports classes of characters that are enclosed in brackets.  

	[:alnum:] - Alphanumeric characters
	[:alpha:] - Alphabetic characters
	[:blank:] - Space and tab
	[:digit:] - Digits
	[:lower:] - Lowercase letters
	[:upper:] - Uppercase letters

There are many more of these in the grep manual.

### Quantifiers
Quantifiers allow you to specify the number of occurances of items that must be present for a match to occur.  

* - zero or more times
$ - preceding item zero or 1 times
+- preceding item 1 or more times
{n} - preceding item exactly n times
{n,} - preceding item at least n time
{,m} - preceding item at most m times
{n,m} - preceding item from n to m times

~~~ bash

# the following would match 'right', 'sright' or 'ssright' and so on

grep 's*right' hello_world.txt

~~~

~~~ bash

#  matches any string that starts with a capital letter and ends with either a ',' or '.' with any number of any characters in between.

grep -E '^[A-Z].*[,.]$' hello_world.txt

#  '.*' means any number of any character

~~~

The ? character makes the preceeding item optional.

~~~ bash

#  will match either 'bright' or 'right'

grep 'b\?right' hello_world.txt

# the '\' is the escape character to idenitfy the '?' as a flag not a character

~~~

Can be used to select any line that has between 3 and 5 digits.

~~~ bash

grep -E '[[:digit:]]{3,5}' hello_world.txt

~~~

## Alternation

Alternation is a simple 'OR'.  The alternation symbol is '|' allows you to specify different possible matches that can be literal strings or expression sets.  

The following code snippet searches for all matches of 'fatal', 'critical' and 'error'.

~~~ bash

# the '\' is used to escape the '|'

grep 'fatal\|error\|critical' hello_world.txt

~~~

## Grouping

## Special backslash expressions

	\b - word boundary
	\< - empty string at the beginning of the word
	\> - empty string at the end of the word
	\w - match a word
	\s - match a space

~~~ bash

grep '\b[ao]bject\b' hello_world.txt

~~~