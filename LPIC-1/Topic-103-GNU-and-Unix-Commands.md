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
- read files 
  - `cat` prints the whole thing, may not be usefull if the file is large 
  - `more` fills only one terminal window at time, enter for one more line, space for whole terminal window refresh 
  - `less` same as more but it can go backwards as well 
- to find used command `history` prints all 
  - or pipe it with `grep` to narrow down the result 
  - in  `/home` there is `.bash_history` with a lot of commands (latest commands are added after session end)
  - `!numberOfCommand` to call it again 
  - `ctrl+r` reverse-i-search to find command i have used before 
  - hidding embarassing stuff `history -c` but the file `.bash_history` stayes there, so delete that as well :) 

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
