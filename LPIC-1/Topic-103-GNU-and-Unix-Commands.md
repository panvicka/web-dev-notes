## Topic 103: GNU and Unix Commands

## 103.1 Work on the command line 
- pwd
- uname
- man
- type
- which
- history
  

## Notes to all of them + random stuff 

- `pwm` shows current folder
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
