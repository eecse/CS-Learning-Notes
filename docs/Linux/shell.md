# The Shell

> How To Use Shell !

## Basic Command
`date`: return current date

`echo`: print something

`echo "Hello World"`

`echo Hello\ World`: when the string contain a space, use `\` to translate

`echo $PATH`: show all the path value

`which` + `command`: return the location of `command`

e.g:`which echo`

## Absolute Path and Relative Path

`pwd`: return current directory
`cd`: enter a directory

`.`: current directory
`..`: parent directory

e.g:

`cd ./temp` :
`cd ../src` :

`cd /` : enter root
`cd ~` : enter current home
`cd -` : toggle between current directory and last directory

`ls` : list files in current directory

`ls -l` : detail of ls

execution of `ls -l /`:

```shell
lrwxrwxrwx   1 root root          7  4月 23 19:24 bin -> usr/bin
drwxr-xr-x   4 root root       4096  5月 19 15:17 boot
drwxrwxr-x   2 root root       4096  4月 23 19:26 cdrom
drwxr-xr-x  20 root root       4140  5月 14 20:42 dev
drwxr-xr-x 143 root root      12288  5月 27 13:31 etc
drwxr-xr-x   3 root root       4096  4月 23 19:27 home
lrwxrwxrwx   1 root root          7  4月 23 19:24 lib -> usr/lib
lrwxrwxrwx   1 root root          9  4月 23 19:24 lib32 -> usr/lib32
lrwxrwxrwx   1 root root          9  4月 23 19:24 lib64 -> usr/lib64
lrwxrwxrwx   1 root root         10  4月 23 19:24 libx32 -> usr/libx32
drwx------   2 root root      16384  4月 23 19:24 lost+found
drwxr-xr-x   2 root root       4096 10月 22  2020 media
drwxr-xr-x   2 root root       4096 10月 22  2020 mnt
drwxr-xr-x   2 root root       4096 10月 22  2020 opt
dr-xr-xr-x 386 root root          0  5月  5 10:14 proc
drwx------   3 root root       4096  4月 25 11:24 root
drwxr-xr-x  32 root root       1040  5月 28 14:04 run
lrwxrwxrwx   1 root root          8  4月 23 19:24 sbin -> usr/sbin
drwxr-xr-x   2 root root       4096  4月 23 19:34 snap
drwxr-xr-x   2 root root       4096 10月 22  2020 srv
-rw-------   1 root root 2147483648  4月 23 19:24 swapfile
dr-xr-xr-x  13 root root          0  5月  5 10:14 sys
drwxrwxrwt  42 root root      12288  5月 28 14:09 tmp
drwxr-xr-x  14 root root       4096 10月 22  2020 usr
drwxr-xr-x  14 root root       4096 10月 22  2020 var
```

## Ls File Format

`lrwxrwxrwx   1 root root          7  4月 23 19:24 bin -> usr/bin`

### First Charater meaning

`l`: symbolic link file;`d`: directory; `-`: normal file; `b`: block; `p`: pipe; `s`: socket; `c`: character

### three character pair

`r`: read
`w`: write
`x`: execute

PS:`-` means you don't have the permission

`first three pair`: permission for user root
`next three pair`: permission for group root
`last three pairn`: permission for everyone else

### File execution command

`mv foo.bar bar.foo` : move(rename) `foo.bar` to `bar.foo`
`cp bar.foo ../` : copy `bar.foo` into parent directory
`rm ../bar.foo`: remove `bar.foo` from parent directory
`mkdir My\ code`: make a folder named `My Code`
`rmdir My\ code/`:remove the folder named `My Code`

`man + command`: the manual description of `command`

`ctrl + l`: move current prompt to top

## Stream

### input and output

`>`: output stream
`<`: input stream

`echo hello > hello.txt`: write string `hello` into hello.txt
`cat hello.txt`: show the content of hello.txt
`cat < hello.txt`: `cat` use hello.txt as input
`cat < hello.txt > hello2.txt`: `cat` from `hello.txt` and redirect to `hello2.txt`
`cat < hello.txt >> hello2.txt`: append `hello.txt` to `hello2.txt`
`echo "something" >> hello2.txt` : append `something` into `hello2.txt`

## Pipe

`|`: pipe

`ls -l / | tail -n1` : return the last line of the `ls -l /`

`curl --head --silent google.com`:

```
HTTP/1.1 301 Moved Permanently
Location: http://www.google.com/
Content-Type: text/html; charset=UTF-8
Date: Fri, 28 May 2021 07:23:47 GMT
Expires: Sun, 27 Jun 2021 07:23:47 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 219
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN
```

`curl --head --silent google.com | grep -i Content-Length`:

return : `Content-Length: 219`

`curl --head --silent google.com | grep -i Content-Length | cut --delimiter= ' ' -f2`:

return: `219`

## Root User

`sudo + command`: do `command` as super user

`/sys/class`: directory contains a lot of sys config files

`echo 500 > /sys/class/backlight/intel_backlight/brightness` : permission denied
`sudo !!` : still permission denied
**why?**
because `sudo` is used on `echo`, while `>` doesn't care about the previous command.

`$`: means you're not running as root
`#`: means you're running as root

`sudo su`: turn into root shell

`tee`:  write something to a file

`echo 1060 | sudo tee brightness`: now brightness is 1060

`xdg-open file`: open a file with correct application

## Exercises

**All classes in this course are accompanied by a series of exercises. Some give you a specific task to do, while others are open-ended, like “try using X and Y programs”. We highly encourage you to try them out.**

We have not written solutions for the exercises. If you are stuck on anything in particular, feel free to send us an email describing what you’ve tried so far, and we will try to help you out.

> 1.For this course, you need to be using a Unix shell like Bash or ZSH. If you are on Linux or macOS, you don’t have to do anything special. If you are on Windows, you need to make sure you are not running cmd.exe or PowerShell; you can use Windows Subsystem for Linux or a Linux virtual machine to use Unix-style command-line tools. To make sure you’re running an appropriate shell, you can try the command `echo $SHELL`. If it says something like `/bin/bash` or `/usr/bin/zsh`, that means you’re running the right program.

> 2.Create a new directory called `missing` under `/tmp`.

> 3.Look up the `touch` program. The man program is your friend.

> 4.Use `touch` to create a new file called `semester` in `missing`.

> 5.Write the following into that file, one line at a time:

```
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
```

**The first line might be tricky to get working. It’s helpful to know that # starts a comment in Bash, and ! has a special meaning even within double-quoted (") strings. Bash treats single-quoted strings (') differently: they will do the trick in this case. See the Bash quoting manual page for more information.**

```shell
# bobby @ BobbydeMBP in /tmp/missing [21:14:21] 
$ touch semester

# bobby @ BobbydeMBP in /tmp/missing [21:14:32] 
$ echo "#!/bin/sh" > semester 
zsh: event not found: /bin/sh

# bobby @ BobbydeMBP in /tmp/missing [21:14:47] C:1
$ cat semester 

# bobby @ BobbydeMBP in /tmp/missing [21:15:01] 
$ echo '#!/bin/sh' > semester 

# bobby @ BobbydeMBP in /tmp/missing [21:15:20] 
$ cat semester 
#!/bin/sh

# bobby @ BobbydeMBP in /tmp/missing [21:15:24] 
$ echo "curl --head --silent https://missing.csail.mit.edu" >> semester 

# bobby @ BobbydeMBP in /tmp/missing [21:16:03] 
$ cat semester 
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
```



> 6.Try to execute the file, i.e. type the path to the script `(./semester)` into your shell and press enter. Understand why it doesn’t work by consulting the output of `ls` (hint: look at the permission bits of the file).

```shell
# bobby @ BobbydeMBP in /tmp/missing [21:16:17] 
$ ./semester 
zsh: permission denied: ./semester

# bobby @ BobbydeMBP in /tmp/missing [21:16:56] C:126
$ ls -l semester 
-rw-r--r--  1 bobby  wheel  61 10  5 21:16 semester
```



> 7.Run the command by explicitly starting the sh interpreter, and giving it the file `semeste`r as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn’t?

> - when we use `sh` command, we take `semester` as input, what we really did was executing `sh` command, and `sh` is executable, so it worked.

```shell
# bobby @ BobbydeMBP in /tmp/missing [21:17:04] 
$ sh semester 
HTTP/2 200 
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Sun, 29 Aug 2021 15:44:11 GMT
access-control-allow-origin: *
etag: "612bab4b-1f31"
expires: Tue, 05 Oct 2021 13:27:51 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 4C3C:7D12:6B9300:749FA1:615C507F
accept-ranges: bytes
date: Tue, 05 Oct 2021 13:17:51 GMT
via: 1.1 varnish
age: 0
x-served-by: cache-hnd18720-HND
x-cache: MISS
x-cache-hits: 0
x-timer: S1633439872.565752,VS0,VE149
vary: Accept-Encoding
x-fastly-request-id: fc0471f99b294b1f9bc9a71654c37e578904967f
content-length: 7985
```



> 8.Look up the `chmod` program (e.g. use `man chmod`).

> 9.Use `chmod` to make it possible to run the command `./semester` rather than having to type sh semester. How does your shell know that the file is supposed to be interpreted using sh? See this page on the shebang line for more information.

```shell
# bobby @ BobbydeMBP in /tmp/missing [21:18:50] 
$ ls -l semester 
-rwxr-xr-x  1 bobby  wheel  61 10  5 21:16 semester

# bobby @ BobbydeMBP in /tmp/missing [21:18:54] 
$ ./semester 
HTTP/2 200 
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Sun, 29 Aug 2021 15:44:11 GMT
access-control-allow-origin: *
etag: "612bab4b-1f31"
expires: Tue, 05 Oct 2021 13:27:51 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 4C3C:7D12:6B9300:749FA1:615C507F
accept-ranges: bytes
date: Tue, 05 Oct 2021 13:18:58 GMT
via: 1.1 varnish
age: 67
x-served-by: cache-hnd18732-HND
x-cache: HIT
x-cache-hits: 1
x-timer: S1633439939.541585,VS0,VE1
vary: Accept-Encoding
x-fastly-request-id: 199d79a9ffc3c879c1367fc960d99ffd126b1b2b
content-length: 7985
```



> 10.Use `|` and `>` to write the “last modified” date output by semester into a file called `last-modified.txt` in your home directory.

```shell
# bobby @ BobbydeMBP in /tmp/missing [21:18:59] 
$ ./semester | grep -i last-modified > ~/last-modified.txt

# bobby @ BobbydeMBP in /tmp/missing [21:19:58] 
$ cat ~/last-modified.txt 
last-modified: Sun, 29 Aug 2021 15:44:11 GMT
```



> 11.Write a command that reads out your laptop battery’s power level or your desktop machine’s CPU temperature from `/sys`. Note: if you’re a macOS user, your OS doesn’t have `sysfs`, so you can skip this exercise.

> - I'm using `MacBook Pro`, so, no can do ):
