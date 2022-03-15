# Shell Scripting

>In this lecture, we will present some of the basics of using bash as a scripting language along with a number of shell tools that cover several of the most common tasks that you will be constantly performing in the command line.

<!--more-->

## Basic Sytax

### Basic value assign

```shell
# bobby @ BobbydeMBP in ~ [10:58:23] 
$ foo=bar

# bobby @ BobbydeMBP in ~ [10:58:28] 
$ echo $foo
bar
```

> **Notice**: spaces are very critical when dealing with bash, because spaces are reserved and will be for separating arguments

```shell
# bobby @ BobbydeMBP in ~ [10:58:32] 
$ foo = bar
zsh: command not found: foo
```

### Print String

> `echo` with double quote `" "` or single quote`' '` can be used to deal with printing `string`

```shell
# bobby @ BobbydeMBP in ~ [11:04:40]
$ echo "Hello"
Hello

# bobby @ BobbydeMBP in ~ [11:09:33] 
$ echo 'World'
World
```

> single quote `' '` won't be replacing the value, while double quote `" "` does it

```shell
# bobby @ BobbydeMBP in ~ [11:13:09] 
$ echo "Value is $foo"
Value is bar

# bobby @ BobbydeMBP in ~ [11:13:19] 
$ echo 'Value is $foo'
Value is $foo
```

### Define Functions

>`bash` also support control flows like `for loops`, `while loops`, combine all that, you can define functions with `bash`

```shell
# mcd.sh
mcd () {
	mkdir -p "$1"
	cd "$1"
}
```

> `$1` stands for the first argument of input, in `bash` we use `$` with number or syntax to represent arguments

```shell
% The result of execution

# bobby @ BobbydeMBP in ~ [13:34:50] 
$ source mcd.sh 

# bobby @ BobbydeMBP in ~ [13:34:55] 
$ mcd test

# bobby @ BobbydeMBP in ~/test [13:35:01] 
```

> - `$0` - Name of the script
> - `$1` to `$9` - Arguments to the script. `$1` is the first argument and so on.
> - `$@` - All the arguments
> - `$#` - Number of arguments
> - `$?` - Return code of the previous command
> - `$$` - Process identification number (PID) for the current script
> - `!!` - Entire last command, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions; you can quickly re-execute the command with sudo by doing `sudo !!`
> - `$_` - Last argument from the last command. If you are in an interactive shell, you can also quickly get this value by typing `Esc` followed by `.`

```shell
% example of $_ - Last argument from the last command

# bobby @ BobbydeMBP in ~ [14:00:42] 
$ rmdir test 

# bobby @ BobbydeMBP in ~ [14:00:48] 
$ echo $_
test

# bobby @ BobbydeMBP in ~ [13:36:48] 
$ mkdir test

# bobby @ BobbydeMBP in ~ [13:36:51] 
$ cd $_

# bobby @ BobbydeMBP in ~/test [13:36:59]
```

```shell
% example of !! - Entire last command

# bobby @ BobbydeMBP in ~ [13:39:51] 
$ mkdir /new
mkdir: /new: Read-only file system

# bobby @ BobbydeMBP in ~ [13:39:54] C:1
$ sudo !!

# bobby @ BobbydeMBP in ~ [13:39:59] C:1
$ sudo mkdir /new
Password:
sudo: no password was provided
sudo: a password is required
```

```shell
% example of $? - Return code of the previous command

# bobby @ BobbydeMBP in ~ [14:02:09] 
$ echo "Hello"
Hello

# bobby @ BobbydeMBP in ~ [14:02:14] 
$ echo $?
0

# bobby @ BobbydeMBP in ~ [14:02:17] 
$ grep foobar mcd.sh 

# bobby @ BobbydeMBP in ~ [14:04:09] C:1
$ echo $?
1

# bobby @ BobbydeMBP in ~ [14:05:11] 
$ true

# bobby @ BobbydeMBP in ~ [14:05:12] 
$ echo $?
0

# bobby @ BobbydeMBP in ~ [14:05:16] 
$ false

# bobby @ BobbydeMBP in ~ [14:05:21] C:1
$ echo $?
1
```

> Return code `0` means it's ok
>
> Return code `1` means it encountered some error while executing

> We can use these features to execute some logical commands

```shell
# bobby @ BobbydeMBP in ~ [14:05:26] 
$ false || echo "Oops fail"
Oops fail

# bobby @ BobbydeMBP in ~ [14:05:55] 
$ true || echo "Will not be printed"

# bobby @ BobbydeMBP in ~ [14:06:09] 
$ false && echo "This will not print"

# bobby @ BobbydeMBP in ~ [14:06:34] C:1
$ false; echo "This will always be printed"
This will always be printed
```

### Getting the output into a variable

> we can use variable to save some output of command

```shell
# bobby @ BobbydeMBP in ~ [14:10:38] 
$ foo=$(pwd)

# bobby @ BobbydeMBP in ~ [14:10:49] 
$ echo $foo
/Users/bobby

# bobby @ BobbydeMBP in ~ [14:10:54] 
$ echo "We are in $foo"
We are in /Users/bobby
```

> we can use `<(command)` to redirect the output of command, for example, we can concatenate output of `ls` current folder and `ls` parent folder.

```shell
# bobby @ BobbydeMBP in ~ [14:11:57] 
$ cat <(ls) <(ls ..)
18-645
Applications
COMP1001
CS61B
CS61C
Comp2611
Desktop
Documents
Downloads
Library
Movies
Music
Pictures
Public
mcd.sh
Shared
bobby
```

> An example script

```shell
#!/bin/bash

echo "Starting program at $(date)" # Date will be substituted

echo "Running program $0 with $# arguments with pid $$"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # When pattern is not found, grep has exit status 1
    # We redirect STDOUT and STDERR to a null register since we do not care about them
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```

> let’s see an example that showcases some of these features. It will iterate through the arguments we provide, `grep` for the string `foobar`, and append it to the file as a comment if it’s not found.

```shell
# bobby @ BobbydeMBP in ~ [14:27:29] C:126
$ chmod +x example.sh 

# bobby @ BobbydeMBP in ~ [14:27:34] 
$ ./example.sh mcd.sh example.sh 
Starting program at 2021年10月 6日 星期三 14时27分41秒 CST
Running program ./example.sh with 2 arguments with pid 4145
File mcd.sh does not have any foobar, adding one

# bobby @ BobbydeMBP in ~ [14:27:41] 
$ cat <(cat mcd.sh) <(cat example.sh) 
mcd () {
	mkdir -p "$1"
	cd "$1"
}
# foobar
#!/bin/bash

echo "Starting program at $(date)" # Date will be substituted

echo "Running program $0 with $# arguments with pid $$"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # When pattern is not found, grep has exit status 1
    # We redirect STDOUT and STDERR to a null register since we do not care about them
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```

> `RE` : Regular expression

```shell
# bobby @ BobbydeMBP in ~ [14:33:03] 
$ mkdir project1 project project42

# bobby @ BobbydeMBP in ~ [14:33:16] 
$ ls *.sh
example.sh mcd.sh

# bobby @ BobbydeMBP in ~ [14:33:29] 
$ ls project*
project:

project1:

project42:
```

> **Note** : we use `?` for single character substitution 

> We can also use curly quote to expand expression

```shell
# bobby @ BobbydeMBP in ~ [14:43:37] 
$ mv image.jpg image.png

# bobby @ BobbydeMBP in ~ [14:44:02] 
$ ls image.*
image.png

# bobby @ BobbydeMBP in ~ [14:44:10] 
$ mv image.{png,jpg}

# bobby @ BobbydeMBP in ~ [14:44:21] 
$ ls image.*
image.jpg
```

> this operation is very powerful, we can use it to creat files/folder in the format we want, etc

```shell
# bobby @ BobbydeMBP in ~/temp [14:46:07] 
$ touch foo{,1,2,10}

# bobby @ BobbydeMBP in ~/temp [14:47:16] 
$ ls
foo   foo1  foo10 foo2

# bobby @ BobbydeMBP in ~/temp [14:48:50] 
$ mkdir project{1,2}

# bobby @ BobbydeMBP in ~/temp [14:49:14] C:1
$ mkdir project{1,2}/src/      

# bobby @ BobbydeMBP in ~/temp [14:49:23] 
$ mkdir project{1,2}/src/test

# bobby @ BobbydeMBP in ~/temp [14:49:25] 
$ touch project{1,2}/src/test/test{1,2,3}.py

# bobby @ BobbydeMBP in ~/temp [14:49:35] 
$ tree .
.
├── project1
│   └── src
│       └── test
│           ├── test1.py
│           ├── test2.py
│           └── test3.py
└── project2
    └── src
        └── test
            ├── test1.py
            ├── test2.py
            └── test3.py

6 directories, 6 files

# bobby @ BobbydeMBP in ~/temp [14:51:51] 
$ mkdir foo bar

# bobby @ BobbydeMBP in ~/temp [14:51:57] 
$ touch {foo,bar}/{a..j}

# bobby @ BobbydeMBP in ~/temp [14:52:20] 
$ touch foo/x bar/y

# bobby @ BobbydeMBP in ~/temp [14:52:34] 
$ diff <(ls foo) <(ls bar)
11c11
< x
---
> y
```

## Bash Script

```python
#!/usr/local/bin/python
import sys
for arg in reversed(sys.argv[1:]):
    print(arg)
```

> this script just print the argument we passed in reversed order

```shell
# bobby @ BobbydeMBP in ~/temp [14:58:18] 
$ python3 script.py a b c d e
e
d
c
b
a
```

> However int the `shebang` line at the top of the script, It is good practice to write shebang lines using the [`env`](https://www.man7.org/linux/man-pages/man1/env.1.html) command that will resolve to wherever the command lives in the system, increasing the portability of your scripts. To resolve the location, `env` will make use of the `PATH` environment variable we introduced in the first lecture. For this example the shebang line would look like `#!/usr/bin/env python`.

> For checking the grammar of shell script, we can use `shellcheck`

```shell
# bobby @ BobbydeMBP in ~/temp [15:04:47] 
$ shellcheck mcd.sh 

In mcd.sh line 1:
mcd () {
^-- SC2148: Tips depend on target shell and yours is unknown. Add a shebang or a 'shell' directive.


In mcd.sh line 3:
	cd "$1"
        ^-----^ SC2164: Use 'cd ... || exit' or 'cd ... || return' in case cd fails.

Did you mean: 
	cd "$1" || exit

For more information:
  https://www.shellcheck.net/wiki/SC2148 -- Tips depend on target shell and y...
  https://www.shellcheck.net/wiki/SC2164 -- Use 'cd ... || exit' or 'cd ... |...
```

> from `man` to `tldr`

> `tldr` is just more readable than `man` page... whatever, just use it

```shell
# bobby @ BobbydeMBP in ~/temp [15:15:00] 
$ tldr tar

tar

Archiving utility.
Often combined with a compression method, such as gzip or bzip2.
More information: <https://www.gnu.org/software/tar>.

- [c]reate an archive and write it to a [f]ile:
    tar cf target.tar file1 file2 file3

- [c]reate a g[z]ipped archive and write it to a [f]ile:
    tar czf target.tar.gz file1 file2 file3

- [c]reate a g[z]ipped archive from a directory using relative paths:
    tar czf target.tar.gz --directory=path/to/directory .

- E[x]tract a (compressed) archive [f]ile into the current directory [v]erbosely:
    tar xvf source.tar[.gz|.bz2|.xz]

- E[x]tract a (compressed) archive [f]ile into the target directory:
    tar xf source.tar[.gz|.bz2|.xz] --directory=directory

- [c]reate a compressed archive and write it to a [f]ile, using [a]rchive suffix to determine the compression program:
    tar caf target.tar.xz file1 file2 file3

- Lis[t] the contents of a tar [f]ile [v]erbosely:
    tar tvf source.tar

- E[x]tract files matching a pattern from an archive [f]ile:
    tar xf source.tar --wildcards "*.html"
```

> it's kind of useful when meeting with new commands, you don't want to remember all the `tag`s for a command, don't you?

## Shell Tools

> When we are finding a file, instead of recursively using `cd` and `ls`, use `find` is way better

```shell
# bobby @ BobbydeMBP in ~/temp [15:19:29] 
$ find . -name src -type d
./project1/src
./project2/src

# bobby @ BobbydeMBP in ~/temp [15:22:50] 
$ find . -path '**/test/*.py' -type f
./project1/src/test/test4.py
./project1/src/test/test1.py
./project1/src/test/test5.py
./project1/src/test/test2.py
./project1/src/test/test3.py
./project2/src/test/test4.py
./project2/src/test/test1.py
./project2/src/test/test5.py
./project2/src/test/test2.py
./project2/src/test/test3.py
```

> You can also execute command with find

```shell
# bobby @ BobbydeMBP in ~/temp [15:25:09] 
$ find . -name "*.tmp" -type f
./project1/src/test/test2.tmp
./project1/src/test/test3.tmp
./project1/src/test/test1.tmp
./project2/src/test/test2.tmp
./project2/src/test/test3.tmp
./project2/src/test/test1.tmp

# bobby @ BobbydeMBP in ~/temp [15:25:24] 
$ find . -name "*.tmp" -type f -exec rm {} \;

# bobby @ BobbydeMBP in ~/temp [15:26:14] 
$ find . -name "*.tmp" -type f  

# bobby @ BobbydeMBP in ~/temp [15:26:18] 
$ echo $?
0
```

> You might think `find` command it quite complex, `fd` is a much simpler command

```shell
# bobby @ BobbydeMBP in ~/temp [15:30:43] C:1
$ fd ".*py"
project1/src/test/test1.py
project1/src/test/test2.py
project1/src/test/test3.py
project1/src/test/test4.py
project1/src/test/test5.py
project2/src/test/test1.py
project2/src/test/test2.py
project2/src/test/test3.py
project2/src/test/test4.py
project2/src/test/test5.py
script.py
```

> use of `grep`

```shell
# bobby @ BobbydeMBP in ~/temp [15:38:47] 
$ grep foobar mcd.sh 
# foobar

# bobby @ BobbydeMBP in ~/temp [15:38:53] 
$ grep -R foobar .
./example.sh:    grep foobar "$file" > /dev/null 2> /dev/null
./example.sh:        echo "File $file does not have any foobar, adding one"
./example.sh:        echo "# foobar" >> "$file"
./mcd.sh:# foobar
```

> We can search pattern in specific file, or we can do thar recursively in give directory

> An alternative is `rg`, check the usage, it's pretty neat

```shell
# Find all python files where I used the requests library
rg -t py 'import requests'
# Find all files (including hidden files) without a shebang line
rg -u --files-without-match "^#!"
# Find all matches of foo and print the following 5 lines
rg foo -A 5
# Print statistics of matches (# of matched lines and files )
rg --stats PATTERN
```

> `history` command can list a history of command you have used, also `control + r` provides a backward search through the command you have used.

```shell
# bobby @ BobbydeMBP in ~/temp [15:55:34] 
$ history | tail -n 10
  765  rg
  766  brew install rg
  767  rg -t py
  768  ""
  769  rg -t py 'import request'
  770  rg -t sh '#'
  771  rg foobar .
  772  history 
  773  clear
  774  history

# bobby @ BobbydeMBP in ~/temp [15:55:46] 
$ rg foobar .         
bck-i-search: rg_
```

> `broot` command! navigate through the directory

**Just Try it out**

## Exercises

> Read [`man ls`](https://www.man7.org/linux/man-pages/man1/ls.1.html) and write an `ls` command that lists files in the following manner

- Includes all files, including hidden files
- Sizes are listed in human readable format (e.g. 454M instead of 454279954)
- Files are ordered by recency
- Output is colorized

A sample output would look like this

```shell
 -rw-r--r--   1 user group 1.1M Jan 14 09:53 baz
 drwxr-xr-x   5 user group  160 Jan 14 09:53 .
 -rw-r--r--   1 user group  514 Jan 14 06:42 bar
 -rw-r--r--   1 user group 106M Jan 13 12:12 foo
 drwx------+ 47 user group 1.5K Jan 12 18:08 ..
```

> `ls -laht` should do the trick

```shell
# bobby @ BobbydeMBP in ~/temp [16:30:30] 
$ ls -laht 
total 64
drwxr-xr-x+ 42 bobby  staff   1.3K 10  6 16:30 ..
drwxr-xr-x  10 bobby  staff   320B 10  6s 16:27 .
drwxr-xr-x   2 bobby  staff    64B 10  6 16:27 .hidden_folder
-rw-r--r--   1 bobby  staff     0B 10  6 16:26 .hidden
drwxr-xr-x   3 bobby  staff    96B 10  6 15:19 project2
drwxr-xr-x   3 bobby  staff    96B 10  6 15:19 project1
-rw-r--r--   1 bobby  staff    85B 10  6 14:55 script.py
-rw-r--r--@  1 bobby  staff    17K 10  6 14:39 image.jpg
-rw-r--r--   1 bobby  staff    44B 10  6 14:27 mcd.sh
-rwxr-xr-x   1 bobby  staff   484B 10  6 14:18 example.sh
```

> Write bash functions `marco` and `polo` that do the following. Whenever you execute `marco` the current working directory should be saved in some manner, then when you execute `polo`, no matter what directory you are in, `polo` should `cd` you back to the directory where you executed `marco`. For ease of debugging you can write the code in a file `marco.sh` and (re)load the definitions to your shell by executing `source marco.sh`.

> Just just a variable `foo` to store the current folder, and `cd` into that folder when we call `polo`

```shell
# marco.sh
marco () {
    foo=$(pwd)
}

polo () {
    cd $foo
}
```

> Say you have a command that fails rarely. In order to debug it you need to capture its output but it can be time consuming to get a failure run. Write a bash script that runs the following script until it fails and captures its standard output and error streams to files and prints everything at the end. Bonus points if you can also report how many runs it took for the script to fail.

```shell
 #!/usr/bin/env bash

 n=$(( RANDOM % 100 ))

 if [[ n -eq 42 ]]; then
    echo "Something went wrong"
    >&2 echo "The error was using magic numbers"
    exit 1
 fi
 echo "Everything went according to plan"
```

> We use a `while-loop` to decide wether to continue depending on last execution's return code, with `cnt=0`, the loop will start, and after each iteration, `$?` Should capture the `scipt`'s return code.

```shell
# test_rare.sh
#!/usr/bin/env bash

rm output 2>/dev/null
cnt=0
while [[  $? -eq 0 ]]
do
    let "cnt++"
    ./$1 >> ./output 2>> ./output
done

let "cnt--"
cat ./output
echo "It took $cnt runs for the script to fail"
```

> As we covered in the lecture `find`’s `-exec` can be very powerful for performing operations over the files we are searching for. However, what if we want to do something with **all** the files, like creating a zip file? As you have seen so far commands will take input from both arguments and STDIN. When piping commands, we are connecting STDOUT to STDIN, but some commands like `tar` take inputs from arguments. To bridge this disconnect there’s the [`xargs`](https://www.man7.org/linux/man-pages/man1/xargs.1.html) command which will execute a command using STDIN as arguments. For example `ls | xargs rm` will delete the files in the current directory.
>
> Your task is to write a command that recursively finds all HTML files in the folder and makes a zip with them. Note that your command should work even if the files have spaces (hint: check `-d` flag for `xargs`).
>
> If you’re on macOS, note that the default BSD `find` is different from the one included in [GNU coreutils](https://en.wikipedia.org/wiki/List_of_GNU_Core_Utilities_commands). You can use `-print0` on `find` and the `-0` flag on `xargs`. As a macOS user, you should be aware that command-line utilities shipped with macOS may differ from the GNU counterparts; you can install the GNU versions if you like by [using brew](https://formulae.brew.sh/formula/coreutils).

```shell
# bobby @ BobbydeMBP in ~/temp/wtf [19:10:53] 
$ find . -name "*.html" -type f -print0 | xargs -0 zip -r compressed.zip
```

> (Advanced) Write a command or script to recursively find the most recently modified file in a directory. More generally, can you list all files by recency?

> **This one is out of my reach**
