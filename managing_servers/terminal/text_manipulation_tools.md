[Home](../../README.md)

#### AWK

#### SED

#### GREP

#### SORT
Sort is a Linux program used for printing lines of input text files and 
concatenation of all files in sorted order. Sort command takes blank space as 
field separator and entire Input file as sort key. It is important to notice 
that sort command don’t actually sort the files but only print the sorted 
output, until your redirect the output.

This article aims at deep insight of Linux ‘sort‘ command with 14 useful 
practical examples that will show you how to use sort command in Linux.

**Sort Command Syntax**
The sort utility expressions take the following form:
```
$ sort [OPTIONS] [FILE_NAME]
```
* OPTIONS - sort options. Use sort --help to view all available options.
* FILE_NAME - file name.
Alternatively you can use
```
$ sort [FILE_NAME] [OPTIONS]
```

**You should note a few thing:**

* When you use sort without any options, the default rules are enforced. It 
  helps to understand the default rules to avoid unexpected outcomes.
* When using sort, your original data is safe. The results of your input are 
  displayed on the command line only. However, you can specify output to a 
  separate file if you wish. More on that later.
*Sort was originally designed for use with ASCII characters. I did not test for
 this, but it is possible that different encodings may produce unexpected results.

**The default rules in the sort command**

These are the default rules when using sort. The first few examples will clarify 
how these priorties are managed. Then we will look at specialized options.

* numbers > letters
* lowercase > uppercase

**Sort in alphabetical order**

The default sort command makes it easy to view information in alphabetical 
order. No options are necessary and even with mixed-case entries, A-Z 
sorting works as expected.
```
$ sort tester.text
```

**Sort on numerical value [option -n]**
This will sort in numerical order if the first letter is number. else it will 
sort based on the first character.
```
$ sort -n tester.text
```

**Sort in reverse order [option -r]**
This will sort in reverse order.
```
$ sort -r tester.text
```

**Random sort [option -R]**
`-R` rearranges output in randomized order.
```
$ sort -R tester.text
```

**Sort by months [option -M]**
Sort also has built in functionality to arrange by month. It recognizes several
formats based on locale-specific information.
```
$ sort -M tester.text
```

**Sort Specific Column [option -k]**
If you have a table in your file, you can use the -k option to specify which 
column to sort.
```
$ sort -k2 tester.text
```
Above will sort the text on the second column in alphabetical order.
```
$ sort -k3n tester.text
```
Above will sort the text by the numerals on the third column.
```
$ sort -k3nr tester.text
```
Same as the above command just that the sort order has been reversed.

**Sort and remove duplicates [option -u]**
`-u` option is used to get the unique objects and sort them.
```
$ sort -u tester.text
```

**Ignore case while sorting [option -f]**
Many modern distros running sort will implement ignore case by default. 
If yours does not, adding the -f option will produce the expected results.
```
$ sort -f tester.text
```

**Sort by human numeric values [option -h]**
This option allows the comparison of alphanumeric values like 1k (i.e. 1000).
```
$ sort -h tester.text
```

#### UNIQ

#### CAT
The `cat` command is one of the most widely used commands in Linux. The name 
of the `cat` command comes from its functionality to con**cat**enate files. It 
can read and concatenate files, writing their contents to the standard output. 
If no file is specified or if the input file name is specified as a single 
hyphen (`-`) it reads from the standard input.

Cat is most commonly used to display the contents of one or multiple text 
files, combine files by appending the contents of one file to the end of 
another file, and create new files.

**Cat Command Syntax**
The cat utility expressions take the following form:
```
$ cat [OPTIONS] [FILE_NAMES]
```
* OPTIONS - cat options. Use cat --help to view all available options.
* FILE_NAMES - Zero or more file names.

Display the contents of the `/etc/issue` file in the terminal:
```
$ cat /etc/issue
```
If file having large number of content that won’t fit in output terminal 
and screen scrolls up very fast, we can use parameters more and less with 
`cat` command as show above.
```
$ cat file.txt | more
$ cat file.txt | less
```
Copy the contents of `file1.txt` to `file2.txt` using the (`>`) operator:
```
$ cat file1.txt > file2.txt
```
> Normally you would use the cp command to copy a file.

If the `file2.txt` file doesn't exist, the command will create it. 
Otherwise, it will overwrite the file.

Use the (`>>`) operator to append the contents of `file1.txt` to `file2.txt`:
```
$ cat file1.txt >> file2.txt
```
> Same as before, if the file is not present, it will be created.

Display contents of a file with line numbers, use the -n option:
```
$ cat -n /etc/lsb-release
```
```
1	DISTRIB_ID=Ubuntu
2	DISTRIB_RELEASE=18.04
3	DISTRIB_CODENAME=bionic
4	DISTRIB_DESCRIPTION="Ubuntu 18.04.1 LTS"
```
Use the `-s` option to omit the repeated empty output lines:
```
$ cat -s file.txt
```
The `-T` option allows you to visually distinguish between tabs and spaces.
```
$ cat -T /etc/hosts
```
```
127.0.0.1^Ilocalhost
127.0.1.1^Iubuntu1804.localdomain
```
> The TAB characters will be displayed as `^I`.

Display the invisible line ending character use the `-e` argument:
```
$ cat -e /etc/lsb-release
```
> The Line endings will be displayed as $.

**Concatenating Files**
When passing two or more file names as arguments to the `cat` command the 
contents of the files will be concatenated. `cat` reads the files in the 
sequence given in its arguments and displays the file’s contents in the 
same sequence.

For example, the following command will read the contents of `file1.txt` and 
`file2.txt` and display the result in the terminal:
```
$cat file1.txt file2.txt
```
You can concatenate two or more text files and write them to a file.The 
following command will concatenate the contents of `file1.txt` and `file2.txt` 
and write them to a new file `combinedfile.txt` using the (`>`) operator :
```
$ cat file1.txt file2.txt > combinedfile.txt
```
If the `combinedfile.txt` file doesn’t exist, the command will create it. 
Otherwise, it will overwrite the file.

To concatenate the contents of `file1.txt` and `file2.txt` and append the 
result to `file3.txt` to use the (`>>`) operator:
```
$ cat file1.txt file2.txt >> file3.txt
```
If the file is not present, it will be created.

#### CUT

#### ECHO

#### FMT

#### TR

#### NL

#### EGREP

#### FGREP

#### WC
wc stands for word count. As the name implies, it is mainly used for counting 
purpose.

* It is used to find out number of lines, word count, byte and characters count 
in the files specified in the file arguments.
* By default it displays four-columnar output.
* First column shows number of lines present in a file specified, second column 
shows number of words present in the file, third column shows number of 
characters present in file and fourth column itself is the file name which are 
given as argument.

**Syntax:**
```
wc [OPTION]... [FILE]...
```
The options below allow you to select which counts are printed.

* `-l`, `--lines` - Print the number of lines.
* `-w`, `--words` - Print the number of words.
* `-m`, `--chars` - Print the number of characters.
* `-c`, `--bytes` - Print the number of bytes.
* `-L`, `--max-line-length` - Print the length of the longest line.

When using multiple options counts are printed in the following order: 
newline, words, characters, bytes, maximum line length.

The `--files0-from=F` option allows `wc` to read input from the files specified 
by NUL-terminated names in file `F`. If `F` is `-` then read names from standard 
input. For example, you can search for files using the find command and provide 
those files as an input to wc:
```
$ find /etc -name 'host*' -printf0 | wc -l --files0-from=-
```
The output will show the number of lines for all files in the `/etc` directory 
whose names start with "host":
```
4 /etc/host.conf
27 /etc/avahi/hosts
1 /etc/hostname
14 /etc/hosts
46 total
```

#### References: 
* awk
  * [likegeeks](https://likegeeks.com/awk-command/) 
  * [Ubuntu Manpage](http://manpages.ubuntu.com/manpages/bionic/man1/awk.1posix.html) 
  * [geeksforgeeks](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/) 
  * [linuxconfig](https://linuxconfig.org/learning-linux-commands-awk) 
* sed
  * []() 
* grep
  * []() 
* sort
  * [Ubuntu manpage](http://manpages.ubuntu.com/manpages/bionic/man1/sort.1.html) 
  * [tecmint](https://www.tecmint.com/sort-command-linux/) 
  * [linuxhandbook](https://linuxhandbook.com/sort-command/) 
* uniq
  * []() 
* cat
  * [Ubuntu manpage](http://manpages.ubuntu.com/manpages/bionic/man1/cat.1.html) 
  * [linuxize](https://linuxize.com/post/linux-cat-command/) 
  * [tecmint](https://www.tecmint.com/13-basic-cat-command-examples-in-linux/)  
* cut
  * [Ubuntu Manpage](http://manpages.ubuntu.com/manpages/bionic/en/man1/cut.1.html) 
  * [linuxize](https://linuxize.com/post/linux-cut-command/) 
  * [ubuntupit](https://www.ubuntupit.com/simple-and-useful-linux-cut-command-in-unix/) 
* echo
  * []() 
* fmt
  * []() 
* tr
  * []() 
* nl
  * []() 
* egrep
  * []() 
* fgrep
  * []() 
* wc
  * [linuxize](https://linuxize.com/post/linux-wc-command/) 
  * [Ubintu manpage](http://manpages.ubuntu.com/manpages/bionic/man1/wc.1.html) 
  * [geeksforgeeks](https://www.geeksforgeeks.org/wc-command-linux-examples/) 
  