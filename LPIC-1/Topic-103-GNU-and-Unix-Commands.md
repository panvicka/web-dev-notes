## Topic 103: GNU and Unix Commands

## 103.1 Work on the command line 
*Lesson 1*
- pwd
- uname
- man
- type
- which
- history
*Lesson 2*
- env
- echo
- var=varValue 
- bash
- export var

## 103.2 Process text streams using filters
- bzcat
- cat
- cut
- head
- less
- md5sum
- nl
- od
- paste
- sed
- sha256sum
- sha512sum
- sort
- split
- tail
- tr
- uniq
- wc
- xzcat
- zcat
- fmt
- pr
- expand
- unexpand
- convert
- join 
- paste
- split
- sort 
- tr
- uniq
- wc

## Notes to all of them + random stuff 

- `pwm` shows current folder
- `cd` without arguments and `cd ~` gets you home, `cd -` toggling between two directories 
- `uname` shows system info
  - `-a` show me everything 
  - `-v` kernel version
  - `-i` hardware platform  
- `touch` creates a file
- `man COMMAND` show manual for a command
  - if you do not remember the command name, `apropos WHATEVER-YOU-ARE-SEARCHING` will try to help you 
- `type` is used to describe how its argument would be translated if used as commands
- `which` returns an absolute path to the command 
- `rm` remove stuff
  - `-r` remove recursively (for folders etc)
- `mv` more stuff FROM TO 
  - used for renaming as well 
  - we can more and rename at the same time 
- `ls`
  - `-l` as a list with more info 
  - `-a` show hidden stuff as well 
  - `-h` human readable sizes 
  - `-i` shows inode numbers 
- read files 
  - `cat` prints the whole thing, may not be usefull if the file is large, `tac` is cat but reversed 
    - `-E` shows end of every line with $ (sometimes spaced at end of the line are a problem)
    - `-T` shows tabs 
    - `-n` line numbers
  - `more` fills only one terminal window at time, enter for one more line, space for whole terminal window refresh 
  - `less` same as more but it can go backwards as well 
- to find used command `history` prints all 
  - or pipe it with `grep` to narrow down the result 
  - in  `/home` there is `.bash_history` with a lot of commands (latest commands are added after session end)
  - `!numberOfCommand` to call it again 
  - `ctrl+r` reverse-i-search to find command i have used before 
  - hidding embarassing stuff `history -c` but the file `.bash_history` stayes there, so delete that as well :) 
- `something | nl` number lines 
- `sed` substitutions 
- `sort` sorting alphabetically, with option `-n` includes numbers as well 
  - `-f` uppercase go first
  - `-r` reverse 
  - `-k 2` sorting based of column 

- linux commands are *hashed* after use, so they can be used quickly again
  - `hash -d` to clean the table

- login as user with `su - user1` 
- run as admin `sudo`
  - sudo session is created, default ca 15 min
  - change timeout in `/etc/sudoers`
  - changes with `visudo` that check if we f***ed up the file or not
  - add `timestamp_timeout` with time (in minutes, 0 - ask always, -1 ask only once)
  - `sudo -k` logout of the sudo session
  - `sudo -i` logs as root  
    - exit with `exit` :) 
- `whoami` to check as who are you logged in 

- in ubuntu has root user no password and you can not log in as root 
- we can set it password with `sudo passwd root` 
- or remove it again with `sudo passwd -l root` 
- first created user has access to sudo 
- newly created users `useradd` do not have sudo by default, we can add them to group
  - list all groups the user is part of `group` 
  - add user to sudo group with `usermod -aG sudo USER`

- show last 20 lines of history with tail `history | tail -20` or just `history 20` 
- `tail -f` file is also refreshing automatically 
- `tail -n 20 fileToCheck` show me last 20 lines of the file 
- combine `head` and `tail` to display a specific line of the file... head of 20 lines | tail -n 1 for line 19 :)
- `od` od command in Linux is used to convert the content of input in different formats with octal format as the default format.This command is especially useful when debugging Linux scripts for unwanted changes or characters. 
- `cut` cut is a command-line utility that allows you to cut parts of lines from specified files or piped data and print the result to standard output. It can be used to cut parts of a line by delimiter, byte position, and character.

 

- show env variables `env` 
- `export var` if you want to access it in a new shell (created with `bash`)
- `export` makes shell variables environment variables
- `set` doesn't set shell nor environment variables
- env variables clean up after reboot or with `unset` 
- `set` gives both environment and shell variables. `env` only gives environment variables, which are passed along to child processes.
- create file with space in name with " `touch "my file"` or with `touch my\ file`
- Escaping using " characters will preserve the special values of the dollar sign, a backtick, and the backslash. Escaping using a ' character, on the other hand, will render all characters as literal.


- STDIN 0 (standart input, keyboard)
- STDOUT 1 (standart output to shell)
  - redirect standart output to a file `1>` or just `>` (will overwrite everything) or with `>>` (attach to) 
- STDERR 2 (error output to shell)
  - redirect with `2>` or `2>>`
- every process running has those 3 channels

- input redirection with `<` for example send a log with email `mail -s "subject" dave < log.txt`
- `cat 2021 > ~/calfile` cave calendar 2021 into home directory 
- `&>` sending standart output and standart error to the same location 
- `tee` always used after pipe ` | tee`, send input to file and to standart output 
- `xargs` command in UNIX is a command line utility for building an execution pipeline from standard input
  - Whilst tools like `grep` can accept standard input as a parameter, many other tools cannot. Using `xargs` allows tools like `echo` and `rm` and `mkdir` to accept standard input as arguments.
  - `-t` show me what you are doing 
  - `-p` show me what are you about to do and prompt me to accept it 
- `-exec` more or less the same as `xargs`, `find . "bla" -exec rm {} \;`
  - `;` or `\;` terminating shell command, will execute multiple commands
  - `+` or `+` terminating shell command with arguments combined together
  - 
```
echo 'one two three' | xargs mkdir
ls
one two three
```

-`mkdir some/files` fails because `some` doesnt exists yet, use `mkdir -p`

## 103.5 Create, monitor and kill processes

Resources I liked
- [Learn Linux, 101: Process execution priorities](https://developer.ibm.com/technologies/linux/tutorials/l-lpic1-103-6/#:~:text=Linux%20and%20UNIX%C2%AE%20systems,)%20using%20the%20%2Dl%20option.)
 
### Notes
 
- everything is a process 
- process has address space (physical address in RAM for data given to it by kernel)
- process data
  - who owns the process
  - what spawned it 
  - priority
  - how much resource 
  - what files & ports is (allowed) using  
  - signal mask 
  - ID (process id, pid)
    - unique ID
    - `init` (/sbin/init) has ID 1, original parent of all processes, runs through all start-up scripts 
    - replaced by `systemd` 
- `top` shows top resource consuming processes 
- `htop` alternative to top, shows are processes 

*Priority* PRI
- kernel-space priority that the Linux Kernel is using. Range 0-139, 0-99 real time and 100-139 for users. 
- can not be changed
*Niceness* NI
- user-space priority to processes, -20 highest prio, 19 lowest prio 
- can be changed 
- relation between niceness and priority `PR = 20 + NI` so `PR = 20 + (-20 to 19)` is 0-39 mapped to 100-139
- increasing niceness increases CPU time (NI+1 is ~ CPU+10%) 
- default niceness is 0, check with `nice` 

- each process has parent, if parent dies all his children are re-parented to init 
- if running process in foreground, it can be suspended with `ctrl+Z` 
  - `fg` unstopped lastly stopped process and brings it to foreground
  - `fg %job-number` (job number) is what it is shown after suspending it 
  - `fg %job-name-or-part-of-it` 
  - `bg` the same but to background 
- starting process in background with `&` at the end
  - returns jpb number and process ID 
  - `jobs -l` shows running job, the one with `+` the the `current one` (command like `fg` without paramters will be applied to it)
- `nohup` process runs even after log out (normally it would stopped because parent is shell and shell is killed after logout, so the process)
- `kill -l` list of all signals 
- processes states 
  - RUNNABLE - process has everything that it needs and can be run next time it gets CPU time 
  - SLEEPING - waiting for something 
  - ZOMBIE - finished and waiting to be killed
  - STOPPED - stopped by SIGSTOP and waiting for SIGCONT to resume 
- `ps aux` list all processes running on a system 
- `ps fax` shows relation between parent and child processes 
- `pgrep` shows filtered processes ID 


## Reg. expression
- basic and extended, check what does the app support 
- bracket expressions `grep b[iag] *`
- range expressions `grep [0-9][0-9]`
- find lines starting/ending `grep ^lisa$`



## LPIC book
- start terminal CTRL+ALT+F2
- in GUI Ubuntu CTRL+ALT+T , all other `term` in search bar 
  - BASH (original Bourne Again Shell)
    - symbolic link `/bin/sh` (use readlink to read it), typically pointing to Bash shell 
  - Dash - no history, command-line editing but faster script execution 
  - KornShell - same as Bash but supports extended functions available in C programming language 
  - tcsh - upgraded C-shell 
  - Z-shell, features from Bash, tcsh and KornShell
  - check what shell is used with `echo $SHELL`, or check bash version with `echo $BASH_VERSION`
  - `uname` 
    - `r` kernel version 
    - `a` all 
- metacharacters `* ? [ ] ' " \ $ ; & ( ) | ^ < >` 
    - To shell quote a single character, use the backslash (\) or use `"` or `'`, use `"` if the text contains `'` 
- files on a linux system are stored within a single directory structure - virtual directory, base is root directory 
- go home with `cd`, `cd ~`, `cd $HOME` 
- recent working directory `cd -` 
- internal and external commands, take them appart with `type` 
    - will tell you if `shell buildin` or path to the command 
- command may be both (available internally and externally). Check the difference, it may produce a different result.
- to check env variabels
    - `set`
    - `env`
    - `printenv`
- You can determine whether your process is currently in a subshell by looking at the data stored in the SHLVL environment variable. A 1 indicates you are not in a subshell, because subshells have higher numbers. Thus, if SHLVL contains a number higher than 1, this indicates you’re in a subshell.
- use unset with care, it is better to set the variable with the previous value 
- search `man` for keywords with `-k` or `apropos` 
- `man` has 9 sections 
  - 1   Executable programs or shell commands
  - 2   System calls (functions provided by the kernel)
  - 3   Library calls (functions within program libraries)
  - 4   Special files (usually found in /dev)
  - 5   File formats and conventions eg /etc/passwd
  - 6   Games
  - 7   Miscellaneous  (including  macro  packages  and  conventions), e.g.  man(7), groff(7)
  - 8   System administration commands (usually only for root)
  - 9   Kernel routines [Non standard]
- in case of `passwd` it can find both command and a file, use `man -s/S/- passwd` to specify 
- if nothing is found, maybe `man` is not updated, try `makewhatis` (old) or `mandb`
- `.bash_history` doesnt have the most recent command, they will be saved after a restart 
  - you can force it to append with `-a`
  - `r` overwrittes history list with commands in history file 
- wiping history
  - `history -c` to delete it, `history -w` to copy the empty history into the file 
- *Nano*, commads with `M-k`, M is a meta key or esc or alt
  - make it a default editor `export EDITOR=nano ` and `export VISUAL=nano` or add them to env file 
- `vi` sometimes starting `vim`, check with `which`, some distros do not have it (but may have vi.tiny)
- cat
  - `-a` show all (like `VEt`)
  - `-n` line numbers 
  - `-s` remove blank lines 
  - `-T` show tabs 
  - `-E` show ends 
  - `-v` nonprintable
    - shown with carrot notation 
- just gluing two files next to each other `paste` 
- `od` show files in octal (default) or another number system 
  - `od cp` show the decoding directly on the text, quite helpful for embedded i guess 
- `split` for splitting large files, with `-l 3` choose how many lines 
- `sort` and include numbers `-n` 
  - `sort -o fileToSort.txt saveToSaveTo.txt` 
- `nl` numbering, also numbering empty lines -ba
- `more` no moving backwards, `less` can 
- `tail -f FILE` will watch log (-f as follow)
- `wc` number of lines, words, bytes 
  - An interesting wc option for troubleshooting configuration files is the -L switch. Generally speaking, line length for a configuration file will be under 150 bytes, though there are exceptions. Thus, if you have just edited a configuration file and that service is no longer working, check the file’s longest line length. A longer than usual line length indicates you might have accidently merged two configuration file lines. An example is shown in Listing 1.43.
- *Text file record* single file line that ends in a newline linefeed LF ($, shonw with `cat -E`)
- *Text file record delimiter* boundaries between different data items within a record 
- `grep`, returns text file records (lines)
  - `-c` show how many records fit 
  - `-E` extendet regex
  - `-i` ignore count 
  - `-r/R` recursive 
  - `-v` invert match 
- `fgrep -f` === `grep -F -f`, `egrep` == `grep -E`
- `grep -v ^$ FILE` to filter out empty lines 
- for exercises with `grep` check this [learnbyexample/Command-line-text-processing](https://github.com/learnbyexample/Command-line-text-processing/tree/master/exercises)