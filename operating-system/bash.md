# Bash and scripting

## profiles

- alias

## bash

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
- reverse search
- cut and paste
- starting scripts
- running processes
- environment variables
  - set ```export <env variable in uppercase>=<value of env variable>```
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
