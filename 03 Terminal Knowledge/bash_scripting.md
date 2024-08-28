[Home](../README.md)

The first line of the shell script file begins with a **"sha-bang" (#!)** which
is not read as a comment, followed by the full path where the shell interpreter
is located. This path, tells the operating system that this file is a set of
commands to be fed into the interpreter indicated. Note that if the path given
at the "sha-bang" is incorrect, then an error message e.g. "Command not
found.", may be the result of the script execution. It is common to name the
shell script with the ".sh" extension. The first line may look like this:

```
#!/bin/bash
```

Adding comments: any text following the "#" is considered a comment

To find out what is currently active shell, and what is its path, type the
highlighted command at the shell prompt (sample responses follow):

```
$ ps | grep $$
987 tty1 00:00:00 bash
```

This response shows that the shell you are using is of type 'bash'. next find
out the full path of the shell interpreter

```
$ which bash
/bin/bash
```

This response shows the full execution path of the shell interpreter. Make sure
that the "sha-bang" line at the beginning of your script, matches this same
execution path.

Print `Hello, World!` in the CLI output

```
$ echo 'Hello, World!'
Hello, World
```

## Variables

Variable name is case-sensitive and can consist of a combination of letters
and the underscore "_". Value assignment is done using the "=" sign. Note that
no space permitted on either side of = sign when initializing variables.

```
$ PRICE_PER_APPLE=5
$ MyFirstLetters=ABC
$ greeting='Hello        world!'
```

Referencing the variables

> A backslash "\" is used to escape special character meaning

```
$ PRICE_PER_APPLE=5
$ echo "The price of an Apple today is: \$HK $PRICE_PER_APPLE"

```

Encapsulating the variable name with `${}` is used to avoid ambiguity

```
$ MyFirstLetters=ABC
$ echo "The first 10 letters in the alphabet are: ${MyFirstLetters}DEFGHIJ"
The price of an Apple today is: $HK 5
```

Encapsulating the variable name with `""` will preserve any white space values

```
$ greeting='Hello        world!'
$ echo $greeting" now with spaces: $greeting"
Hello world! now with spaces: Hello        world!
```

> on `ZSH`, you don't need to encapsulate, white spaces are preserved

Variables can be assigned with the value of a command output. This is referred
to as substitution. Substitution can be done by encapsulating the command with
`` (known as back-ticks) or with `$()`

```
$ FILELIST=`ls`
$ FileWithTimeStamp=/tmp/my-dir/file_$(/bin/date +%Y-%m-%d).txt
$ echo $FileWithTimeStamp
/tmp/my-dir/file_2024-08-21.txt
```

Note that when the script runs, it will run the command inside the `$()`
parenthesis and capture its output.

## Exercise

The target of this exercise is to create a string, an integer, and a complex
variable using command substitution. The string should be named BIRTHDATE and
should contain the text "Jan 1, 2000". The integer should be named Presents
and should contain the number 10. The complex variable should be named BIRTHDAY
and should contain the full weekday name of the day matching the date in
variable BIRTHDATE e.g. Saturday. Note that the 'date' command can be used to
convert a date format into a different date format. For example, to convert
date value, $date1, to day of the week of date1, use:

```
$ date -d "$date1" +%A
```

### Solution

```
$ BIRTHDATE="Jan 1, 2000"
$ Presents=10
$ BIRTHDAY=$(date -d "$BIRTHDATE" +%A)
$ echo $BIRTHDAY
Saturday
```

## Arguments

Arguments can be passed to the script when it is executed, by writing them as
a space-delimited list following the script file name.

Inside the script, the $1 variable references the first argument in the
command line, $2 the second argument and so forth. The variable $0 references
to the current script. In the following example, the script name is followed
by 6 arguments.

`my_shopping.sh` file contains below code.

```bash
#!/bin/bash
echo "File name is "$0 # holds the current script
echo $3 # $3 holds banana
Data=$5
echo "A $Data costs just $6."
echo $#
```

Executing the script on terminal with arguments,

```
$ bash my_shopping.sh apple 5 banana 8 "Fruit Basket" 15
File name is my_shopping.sh
banana
A Fruit Basket costs just 15
6
```

The variable `$#` holds the number of arguments passed to the script

The variable `$@` holds a space delimited string of all arguments passed to
the script.

## Arrays

An array can hold several values under one name. Array naming is the same as
variables naming. An array is initialized by assign space-delimited values
enclosed in ()

```
$ my_array=(apple banana "Fruit Basket" orange)
$ new_array[2]=apricot
```

Array members need not be consecutive or contiguous. Some members of the array
can be left uninitialized.

The total number of elements in the array is referenced by `${#arrayname[@]}`

```
$ my_array=(apple banana "Fruit Basket" orange)
$ echo  ${#my_array[@]}                   # 4
```

The array elements can be accessed with their numeric index. The index of the
first element is 0.

```
$ my_array=(apple banana "Fruit Basket" orange)
$ echo ${my_array[3]}                     # orange - note that curly brackets are needed
# adding another array element
$ my_array[4]="carrot"                    # value assignment without a $ and curly brackets
$ echo ${#my_array[@]}                    # 5
$ echo ${my_array[${#my_array[@]}-1]}     # carrot
```

### Exercise

In this exercise, you will need to add numbers and strings to the correct
arrays. You must add the numbers 1,2, and 3 to the "numbers" array, and the
words 'hello' and 'world' to the strings array.

You will also have to correct the values of the variable NumberOfNames and the
variable second_name. NumberOfNames should hold the total number of names in
the NAMES array, using the $# special variable. Variable second_name should
hold the second name in the NAMES array, using the brackets operator [ ]. Note
that the index is zero-based, so if you want to access the second item in the
list, its index will be 1.

### Solution

```
#!/bin/bash
NAMES=( John Eric Jessica )
# write your code here
NUMBERS=( 1 2 3 )
STRINGS=( "hello" "world" )
NumberOfNames=${#NAMES[@]}
second_name=${NAMES[1]}
echo ${NUMBERS[@]}
echo ${STRINGS[@]}
echo "The number of names listed in the NAMES array: $NumberOfNames"
echo "The second name on the NAMES list is:" ${second_name}
```

## Arithmetic Operators

Simple arithmetics on variables can be done using the arithmetic expression:
$((expression)), BTW, `$/${}` is unnecessary on arithmetic variables.

```
$ A=3
$ B=$((100 * A + 5)) # 305
```

The basic operators are:

**_a+ b_** addition (a plus b)

**_a - b_** subtraction (a minus b)

**_a * b_** multiplication (a times b)

**_a / b_** division (integer) (a divided by b)

**_a % b_** modulo (the integer remainder of a divided by b)

**_a ** b_** exponentiation (a to the power of b)

### Exercise

In this exercise, you will need to calculate to total cost (variable TOTAL)
of a fruit basket, which contains 1 pineapple, 2 bananas and 3 watermelons.
Don't forget to include the cost of the basket....

```
#!/bin/bash 
COST_PINEAPPLE=50
COST_BANANA=4
COST_WATERMELON=23
COST_BASKET=1
TOTAL= ?
echo "Total Cost is $TOTAL"
```

### Solution

```
#!/bin/bash
COST_PINEAPPLE=50
COST_BANANA=4
COST_WATERMELON=23
COST_BASKET=1
TOTAL=$(( COST_PINEAPPLE * 1 + COST_BANANA * 2 + COST_WATERMELON * 3 + COST_BASKET * 1 ))

echo "Total Cost is $TOTAL"
```

## Basic String Operations

The shell allows some common string operations which can be very useful for
script writing.

### String Length

```
#       1234567890123456
$ STRING="this is a string"
$ echo "${#STRING}"            # 16
```

### Index

Find the numerical position in $STRING of any single character in $SUBSTRING
that matches. Note that the 'expr' command is used in this case.

```
$ STRING="this is a string"
$ SUBSTRING="hat"
$ expr index "$STRING" "$SUBSTRING"     # 1 is the position of the first 't' in $STRING
# latest: https://github.com/koalaman/shellcheck/wiki/SC2308
$ _sub=${var%%[$SUBSTRING]*}
$ indx=$((${#_sub}+1))
$ echo "$indx"
```

### Substring Extraction

Extract substring of length $LEN from $STRING starting after position $POS.
Note that first position is 0.

```
$ STRING="this is a string"
$ POS=1
$ LEN=3
$ echo "${STRING:$POS:$LEN}"   # his
```

If :$LEN is omitted, extract substring from $POS to end of line

```
$ STRING="this is a string"
$ echo "${STRING:1}"           # $STRING contents without leading character
$ echo "${STRING:12}"          # ring
```

### Simple data extraction example:

```
# Code to extract the First name from the data record
$ DATARECORD="last=Clifford,first=Johnny Boy,state=CA"
$ COMMA1=`expr index "$DATARECORD" ','`  # 14 position of first comma
$ CHOP1FIELD=${DATARECORD:$COMMA1}       #
$ COMMA2=`expr index "$CHOP1FIELD" ','`
$ LENGTH=`expr $COMMA2 - 6 - 1`
$ FIRSTNAME=${CHOP1FIELD:6:$LENGTH}      # Johnny Boy
$ echo $FIRSTNAME

# SC2003, SC2308, SC2086 
$ DATARECORD="last=Clifford,first=Johnny Boy,state=CA"
$ tmp=${DATARECORD%%,*}
$ COMMA1=$((${#tmp}+1))
$ CHOP1FIELD=${DATARECORD:$COMMA1}
$ tmp=${CHOP1FIELD%%,*}
$ COMMA2=$((${#tmp}+1))
$ LENGTH=$((COMMA2 -6 - 1))
$ FIRSTNAME=${CHOP1FIELD:6:$LENGTH}      # Johnny Boy
$ echo "$FIRSTNAME"
```

### Substring Replacement

```
$ STRING="to be or not to be"
```

Replace first occurrence of substring with replacement

```
$ STRING="to be or not to be"
$ echo "${STRING[@]/be/eat}"        # to eat or not to be
```

Replace all occurrences of substring

```
$ STRING="to be or not to be"
$ echo "${STRING[@]//be/eat}"        # to eat or not to eat
```

Delete all occurrences of substring (replace with empty string)

```
$ STRING="to be or not to be"
$ echo "${STRING[@]// not/}"        # to be or to be
```

Replace occurrence of substring if at the beginning of $STRING

```
$ STRING="to be or not to be"
$ echo "${STRING[@]/#to be/eat now}"    # eat now or not to be
```

Replace occurrence of substring if at the end of $STRING

```
$ STRING="to be or not to be"
$ echo "${STRING[@]/%be/eat}"        # to be or not to eat
```

replace occurrence of substring with shell command output

```
$ STRING="to be or not to be"
$ echo "${STRING[@]/%be/be on $(date +%Y-%m-%d)}"    # to be or not to be on 2012-06-14

```

### Exercise

In this exercise, you will need to change Warren Buffett's known saying. First
create a variable ISAY and assign it the original saying value. Then re-assign
it with a new changed value using the string operations and following the 4
defined changes: Change1: replace the first occurrence of 'snow' with 'foot'.
Change2: delete the second occurrence of 'snow'. Change3: replace 'finding'
with 'getting'. Change4: delete all characters following 'wet'. Tip: One way to
implement Change4, if to find the index of 'w' in the word 'wet' and then use
substring extraction.

### Solution

```
#!/bin/bash

BUFFETT="Life is like a snowball. The important thing is finding wet snow and a really long hill."
ISAY=$BUFFETT
c1=${ISAY[*]/snow/foot}
c2=${c1[*]//snow/}
c3=${c2[*]//finding/getting}
# slice the string until wet
x=${c3%%wet*}
# get length+1
index=$((${#x}+1))
ISAY=${c3::index+2}
echo "$ISAY"
```

## Decision-Making

As in popular programming languages, the shell also supports logical
decision-making.

The basic conditional decision-making construct is:

```
if [ expression ]; then

code if 'expression' is true

fi
```

For example,

```
NAME="John"
if [ "$NAME" = "John" ]; then
  echo "True - my name is indeed John"
fi
```

It can be expanded with 'else'

```
NAME="Bill"
if [ "$NAME" = "John" ]; then
  echo "True - my name is indeed John"
else
  echo "False"
  echo "You must mistaken me for $NAME"
fi
```

It can be expanded with 'elif' (else-if)

```
NAME="George"
if [ "$NAME" = "John" ]; then
  echo "John Lennon"
elif [ "$NAME" = "George" ]; then
  echo "George Harrison"
else
  echo "This leaves us with Paul and Ringo"
fi
```

The expression used by the conditional construct is evaluated to either true or
false. The expression can be a single string or variable. A empty string or a
string consisting of spaces or an undefined variable name, are evaluated as
false. The expression can be a logical combination of comparisons: negation is
denoted by !, logical AND (conjunction) is denoted by &&, and logical OR
(disjunction) is denoted by ||. Conditional expressions should be surrounded by
double brackets [[ ]].

### Types of numeric comparisons

```
comparison   Evaluated to true when
$a -lt $b    $a < $b
$a -gt $b    $a > $b
$a -le $b    $a <= $b
$a -ge $b    $a >= $b
$a -eq $b    $a is equal to $b
$a -ne $b    $a is not equal to $b
```

### Types of string comparisons

```
comparison      Evaluated to true when
"$a" = "$b"     $a is the same as $b
"$a" == "$b"    $a is the same as $b
"$a" != "$b"    $a is different from $b
-z "$a"         $a is empty
```

> **note 1**: whitespace around = is required  
> **note 2**: use "" around string variables to avoid shell expansion of
> special characters as *

### Logical combinations

```
if [[ $VAR_A[0] -eq 1 && ($VAR_B = "bee" || $VAR_T = "tee") ]] ; then
    command...
fi
```

### case structure

```
case "$variable" in
    "$condition1" )
        command...
    ;;
    "$condition2" )
        command...
    ;;
esac
```

simple case bash structure

```
mycase=1
case $mycase in
    1) echo "You selected bash";;
    2) echo "You selected perl";;
    3) echo "You selected phyton";;
    4) echo "You selected c++";;
    5) exit
esac
```

## oops

### bash for loop

```
# basic construct
for arg in [list]
do
 command(s)...
done
```

For each pass through the loop, arg takes on the value of each successive value
in the list. Then the command(s) are executed.

```
# loop on array member
NAMES=(Joe Jenny Sara Tony)
for N in ${NAMES[@]} ; do
  echo "My name is $N"
done

# loop on command output results
for f in $( ls prog.sh /etc/localtime ) ; do
  echo "File is: $f"
done
```

### bash while loop

```
# basic construct
while [ condition ]
do
 command(s)...
done
```

The while construct tests for a condition, and if true, executes commands. It
keeps looping as long as the condition is true.

```
COUNT=4
while [ $COUNT -gt 0 ]; do
  echo "Value of count is: $COUNT"
  COUNT=$(($COUNT - 1))
done
bash until loop
# basic construct
until [ condition ]
do
 command(s)...
done
```

The until construct tests for a condition, and if false, executes commands. It
keeps looping as long as the condition is false (opposite of while construct)

```
COUNT=1
until [ $COUNT -gt 5 ]; do
  echo "Value of count is: $COUNT"
  COUNT=$(($COUNT + 1))
done
```

### "break" and "continue" statements

break and continue can be used to control the loop execution of for, while and
until constructs. continue is used to skip the rest of a particular loop
iteration, whereas break is used to skip the entire rest of loop. A few
examples:

```
# Prints out 0,1,2,3,4

COUNT=0
while [ $COUNT -ge 0 ]; do
  echo "Value of COUNT is: $COUNT"
  COUNT=$((COUNT+1))
  if [ $COUNT -ge 5 ] ; then
    break
  fi
done

# Prints out only odd numbers - 1,3,5,7,9
COUNT=0
while [ $COUNT -lt 10 ]; do
  COUNT=$((COUNT+1))
  # Check if COUNT is even
  if [ $((COUNT % 2)) = 0 ] ; then
    continue
  fi
  echo $COUNT
done
```

### Exercise

In this exercise, you will need to loop through and print out all even numbers
from the numbers list in the same order they are received. Don't print any
numbers that come after 237 in the sequence.

```
#!/bin/bash

NUMBERS=(951 402 984 651 360 69 408 319 601 485 980 507 725 547 544 615 83 165 141 501 263 617 865 575 219 390 237 412 566 826 248 866 950 626 949 687 217 815 67 104 58 512 24 892 894 767 553 81 379 843 831 445 742 717 958 609 842 451 688 753 854 685 93 857 440 380 126 721 328 753 470 743 527)
```

### Solution

```
#!/bin/bash

NUMBERS=(951 402 984 651 360 69 408 319 601 485 980 507 725 547 544 615 83 165 141 501 263 617 865 575 219 390 237 412 566 826 248 866 950 626 949 687 217 815 67 104 58 512 24 892 894 767 553 81 379 843 831 445 742 717 958 609 842 451 688 753 854 685 93 857 440 380 126 721 328 753 470 743 527)

for num in "${NUMBERS[@]}"; do
  if [[ $num -eq 237 ]]; then
    break
  fi
  if [[ $(($num % 2)) = 0 ]]; then
    echo "$num"
  else
    continue
  fi
done
```

## References

* [learnshell.org](https://www.learnshell.org/)