# AWK Cheatsheet
AWK is a scripting language used for manipulating data and generating reports.It is mainly built for reading csv style files.

## Syntax
```
$ awk '<Pattern> {<Action>}' FileName
```
Let's first display the text file where we will be working on:
```
$ awk '{print}' text.txt
10 Sachin Tendulkar 200
Hello world Ubuntu 20
13 Rishav 1
January
333
MKBHD Ryzen 4800H
M1 Max 
Git Hub 2021
November 2
SUzuki Hayabusa
Rohit Sharma 264
7 MS Dhoni 183
Nvidia RTX 3090 Ti 12GB

```
## Lets see a some basic example:
- #### Searching some pattern in text file:
    Searching Sachin in text.txt file
  
```
$ awk '/Sachin/ {print}' text.txt
10 Sachin Tendulkar 200
```
  We can also print the particular column we can just put $ followed by 1,2,3 as per the column number:
```
$ awk '{print $1 }' text.txt
  10
  Hello
  13
  January
  333
  MKBHD
  M1
  Git
  November
  SUzuki
  Rohit
  7
  Nvidia
```
  What if we want to print only those rows which has numeric values, we can do it by putting [0-9]:
```
$ awk '/[0-9]/ {print}' text.txt
  10 Sachin Tendulkar 200
  Hello world Ubuntu 20
  13 Rishav 1
  333
  MKBHD Ryzen 4800H
  M1 Max 
  Git Hub 2021
  November 2
  Rohit Sharma 264
  7 MS Dhoni 183
  Nvidia RTX 3090 Ti 12GB
```
To print rows with numeric value just in first field, we can use ^:
```
$ awk '/^[0-9]/ {print}' text.txt
  10 Sachin Tendulkar 200
  13 Rishav 1
  333
  7 MS Dhoni 183*
```
- ### Relational Expression patterns
  We can use various operators to print the file:
  To print the record whose second field contains “ish” you would type:
```
$ awk '$2 ~ /ish/ { print }' text.txt
  13 Rishav 1
```
  Similarly we can use !~ for printing record that not include certain pattern:
```
$ awk '$2 !~ /ish/ { print }' text.txt
  10 Sachin Tendulkar 200
  Hello world Ubuntu 20
  January
  333
  MKBHD Ryzen 4800H
  M1 Max 
  Git Hub 2021
  November 2
  SUzuki Hayabusa
  Rohit Sharma 264
  7 MS Dhoni 183
  Nvidia RTX 3090 Ti 12GB
```
Let's Print another file which we will be using for numeric operation:
```
$ cat sum.txt
  234
  212
  434
  122
  985
  320

```
Let's use > and < operator:
```
$ awk '$1 > 250 { print $1 }' sum.txt
  434
  985
  320
```
```
$ awk '$1 < 250 { print $1 }' sum.txt
  234
  212
  122
```
- ### Range Patterns
All records starting with a record that matches the first pattern until a record that matches the second pattern are matched.
```
$ awk '/MKBHD/,/Dhoni/ { print }' text.txt
  MKBHD Ryzen 4800H
  M1 Max 
  Git Hub 2021
  November 2
  SUzuki Hayabusa
  Rohit Sharma 264
  7 MS Dhoni 183
```
The patterns can also be relation expressions.
```
$ awk '$1 == 434, $1 == 320 { print $1 }' sum.txt
  434
  122
  985
  320
```
- ### Special Pattern
AWK include some sepecial pattern like BEGIN and END.
BEGIN- is used to perform action before data are processed.
END-  is used to perform action after data are processed.
```
$ awk 'BEGIN{print "Some random data:"}; {print}' text.txt
  Some random data:
  10 Sachin Tendulkar 200
  Hello world Ubuntu 20
  13 Rishav 1
  January
  333
  MKBHD Ryzen 4800H
  M1 Max 
  Git Hub 2021
  November 2
  SUzuki Hayabusa
  Rohit Sharma 264
  7 MS Dhoni 183
  Nvidia RTX 3090 Ti 12GB
```

Lets used the END operation to find the sum of enteries in sum.txt file
```
$ cat sum.txt
  234
  212
  434
  122
  985
  320

$ awk '{s+=$1} END{ printf "%d \n",s}' sum.txt
2307

```
- ### Combining pattern
Awk is used to combines patterns using && and ||:
```
$ awk '$1> 9 && $4 > 20 { print $1 }' text.txt
  10 Sachin Tendulkar 200
  Nvidia RTX 3090 Ti 12GB
```
- ### Built-in variables
Awk has a number of built-in variables that contain useful information and allows you to control how the program is processed.
- NF - The number of fields in the record.
- NR - The number of the current record.
- FILENAME - The name of the input file that is currently processed.
- FS - Field separator.
- RS - Record separator.  

Lets diplay Filename and number of lines it has
```
$ awk 'END { print "File",FILENAME,"has",NR,"lines"}' sum.txt
  File sum.txt has 6 lines
```
Awk can also use the -F option to change the field separator:
```
$ cat field.txt
  10: Sachin Tendulkar 200
  Hello: world Ubuntu 20
  13: Rishav 1
  333
  MKBHD: Ryzen 4800H
  M1: Max 
$ awk -F ":" '{ print $1 }' field.txt
  10
  Hello
  13
  333
  MKBHD
  M1
```

## AWK Actions
We can print multiple items with the use of separators(,)
  $ awk '{ print $1, $3, $5 }' text.txt
```
$ awk '{ print $2, $1, $3 }' text.txt
  Sachin 10 Tendulkar
  world Hello Ubuntu
  Rishav 13 1
  January 
  333 
  Ryzen MKBHD 4800H
  Max M1 
  Hub Git 2021
  2 November 
  Hayabusa SUzuki 
  Sharma Rohit 264
  MS 7 Dhoni
  RTX Nvidia 3090

```
If you don't use separators and put space instead, then there will be no space between the item
