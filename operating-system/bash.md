# Bash and scripting

## profiles

- files
  - profiles
    - .bash_profile and .profile which are only run at the start of a new login shell. (bash -l)
    - run once
  - .bashrc
    - is a shell script that Bash runs whenever it is started interactively. It initializes an interactive shell session. You can put any command in that file that you could type at the command prompt.
    - You put commands here to set up the shell for use in your particular environment, or to customize things to your preferences. A common thing to put in .bashrc are aliases that you want to always be available.
      -  place where you can set up variables, functions and aliases, define your (PS1) prompt and define other settings that you want to use every time you open a new terminal window.
    - .bashrc runs on every interactive shell launch
      - `> bash` in terminal will run bashrc

- alias
  - `alias mqc="mvn clean verify"`
- environment variables
  - set ```export <env variable in uppercase>=<value of env variable>```

## bash commands

- ls
  - flags -al
- cd
  - multiple folders
  - to root
- copy ```cp```
- move ```mv```
  - rename
- ```.```
- cat
  - combining text
  - showingfile
- less
  - searching in less
- ```head -3 <filename>```
  - show first n number of lines
- ```tail -3 <filename>```
  - show last n lines
  - '''tail -f <filename>
    - follow end of file, great for following logs as a program is run
  - ```/<regex search term>``` searching within less
- https://www.lifewire.com/what-to-know-less-command-4051972
- echo
- grep
- find
- create file
- `xkill`
  - Then click on program that wont shutdown
- reverse search
- cut and paste
- starting scripts
- running processes
- environment variables
  - print ```echo $<name of env  variable>```
    - This will return nothing if env is not defined
  - Path

- ```echo <something``` printing to console
- piping
- whoami
- permissions
- chmod
- chown
- symlink
- sudo
- mkdir
- rmdir
  - rmdir -r
- rm
  - rm -f
- chain command &&
- watch
- view ports in use
  - kill ports
- View processes
  - kill processes
- Ziping and unzipping files
- Curl
- top
  - monitoring processes, mem usuage etc
- du
  - monitoring disk usuage
  - `du -sh *`` summarises disk usages of the files in the current directory we use
  - `du -sh .[!.]* *` to include hidden files
- df -h
  - summarises disk usage of each harddrive
- source ./bashrc
  - to run bash profile, if updating it


## Permissions

## makefiles

## Links

- http://www.ee.surrey.ac.uk/Teaching/Unix/
- https://learncodethehardway.org/unix/
- https://github.com/Idnan/bash-guide
- https://github.com/enkidevs/curriculum/wiki/Linux-Topic
