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

## References

* [learnshell.org](https://www.learnshell.org/)