# AWK Cheatsheet
AWK is a scripting language used for manipulating data and generating reports.It is mainly built for reading csv style files.

## Syntax
```
$ awk '<Pattern> {<Action>}' FileName
```
Let's first display the text file where we will be working on:

Lets see a most basic example to search a pattern in a text file.
```
$ awk '/sachin/
