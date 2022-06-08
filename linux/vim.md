# Key Bindings
### Resources referenced
[vim/python ](https://realpython.com/vim-and-python-a-match-made-in-heaven/#nix-linux)

## Modes

1.  Normal - For performaing actions like navigation, substitutions, copy, paste and delete.
2.  Insert - For inserting text like a normal text editor
3.  Visual - ? What the hell is this ? 

## Navigating

h - left
j - down
k - up
l - right

## General use
### Deleting

x - in normal mode x delets a character
dw - in normal mode dw deletes an entire word.  The cursor needs to be at the beginning of the word.
d$ - in normal mode d$ deletes to the end of the line.

adding a count into the command repeats it.

d2w deletes that many words:w


### Using a count for a motion

Typing a 2 before a motion repeats it that many times.

2w moves the cursor two words forward
3e moves the cursor to the end of the third word forward
0 moves the cursor to the start of the lin


### Operating on files

Delete a whole line

dd deletes and entire line

2dd deletes 2 entire lines 

## Extensions
### Vundle
[Vundle](https://github.com/VundleVim/Vundle.vim) is an extension manager.

~~~

# adding plugins after installiing

:PluginInstall


~~~

### Split layouts

If you open a file with the :sp <file name> the file will be opened with a vertical split.

Alternatively, the :vs <file name> will split verticaally.



