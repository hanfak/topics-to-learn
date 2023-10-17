# Bash and scripting

- [Bash and scripting](#bash-and-scripting)
  * [profiles](#profiles)
  * [bash commands](#bash-commands)
    + [Help/Manuals](#helpmanuals)
    + [Tab completion](#tab-completion)
    + [Pipes ](#pipes)
    + [cd ](#cd)
    + [pwd](#pwd)
    + [ls ](#ls)
    + [mv](#mv)
    + [cp](#cp)
    + [file](#file)
    + [symlinks](#symlinks)
    + [create file or directory](#create-file-or-directory)
    + [deleting file or directory](#deleting-file-or-directory)
    + [zipping and unzipping](#zipping-and-unzipping)
    + [find ](#find)
    + [locate ](#locate)
    + [clear](#clear)
    + [Bash history](#bash-history)
    + [diff](#diff)
    + [cat ](#cat)
    + [less](#less)
    + [more](#more)
    + [echo](#echo)
    + [grep](#grep)
    + [sed](#sed)
    + [xkill](#xkill)
    + [show processes](#show-processes)
    + [Permissions](#permissions)
    + [Curl](#curl)
    + [cron](#cron)
    + [shutdown](#shutdown)
    + [environment variables](#environment-variables)
    + [running scripts](#running-scripts)
    + [Fun](#fun)
    + [Others](#others)
  * [makefiles](#makefiles)
  * [vi ](#vi)
  * [Links](#links)

- Born again shell
- Interpts your commands and feeds it to the kernal

## Shortcuts 

- to got beginning of line - `ctrl + a`
- to got end of line - `ctrl + e`
- clear screen  - `ctrl + l`
- terminate command - `ctrl + c`
- previous command - `arrow up`
- later command - `arrow down`
- Exit out of shell - `ctrl + d`

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
  - Can use alias/shortcuts for commands and place them in your profile
  - `alias mqc="mvn clean verify"`
- environment variables
  - set ```export <env variable in uppercase>=<value of env variable>```

## bash commands

### Help/Manuals

- Examples - not all commands will have these help commands
  - `man ps`
  - `ps --help`
  - `ps --help simple`
  - `ps -h`
  - `ps help`
  - `info ps`

### Tab completion

- can use tab to complete a command, or give options for the command
- Instead of searching contents of directory first (ie cd then ls)
- examples 
  - `cd /dir/h` then tab, will autocomplete if one exists -> `cd /dir/hello`
    - if multiple options exists -> will show them below `hello hi hop`

### Pipes 

- Takes the output of one command passes it as the input to the next command
- Can keep chaining
- Examples
  - `echo 123 | rev` -> `321`
  - `echo 123 | rev | rev` -> `123`

### cd 

- change directories 
- navigate to dir directory from current directory: `cd dir`
- navigate to directory using home path: `cd ~/dir`
- navigate to directory using full path: `cd /home/temp/dir`
- navigate to directory using env variable: `cd $BASE/temp/dir`
- navigate to home directory: `cd`
- navigate to previous directory: `cd -`
- navigate up a directory: `cd ..`
  - navigate up two directories up: `cd ../..`
  - navigate up a directory and down to another: `cd ../childDir`

### pwd

- `pwd` - shows current directory

### ls 

- shows contentst of directory
- `ls` - shows files and directories in current directory
- `ls dir/child` - shows files and directories, from directory dir/child in current directory
- `ls /dir/child` - shows files and directories, from directory dir/child from root
- `ls -a` - shows files and directories, including hidden ones
- `ls -l` - shows one per line, showing file or directory permission, Owner and Group Name, File size, created/modified date and time, file/folder name"
  - `ls -l file.txt` - shows detail of specific file
  - `ls -l dir/` - shows detail of all files in directory
  - `ls -lh` - output is human readable, useful when details are given, shows you can combine flags
- `ls -F` - shows files and directories, but directories will have trialing /
- `ls -lR` - shows files and directories, of current and child directories
- `ls -lS` - shows files and directories, sorted by size
- `unzip -l dir.zip` - shows contents of zipped file

### mv

- moves a file or directory from one location to another
- Change the name of a file
- Examples
  - Change name of file: `mv file.txt newFile.txt` 
  - Change name of directory: `mv dir newDir` 
  - Move directory to similar format: `mv dir{1,11}` 
  - Move file from current location to a directory: `mv file.txt /tmp`
  - Move multiple files: `mv file1 file2 dir1`
  - Move all files and directories to another, not dot files: `mv ~/dir/* ~/dir1/`
  - Move all files and directories to another: `(shopt -s dotglob; mv ~/dir/* ~/dir1)`
  - Move all files but subfolders: `find ~/dir/ -type f -print0 | xargs -0 mv -t ~/dir1`
  - Move all files of type to a directory: `mv *.pdf ~/dir`
  - Move file from specific location to a directory: `mv /current/file.txt /tmp`
  - Move directory to another directory: `mv dir1 dir2`
  - Overwrite a file on moving, will ask for confirmation: `mv -i file.txt newFile.txt`
  - Force a file to be moved, especially if it is read only: `mv -f file.txt newFile.txt`
  - Dont move a file if it already exists at new location: `mv -n file.txt newFile.txt`
  - Back up a file, at the current location, this will append a ~: `mv -b file1 .`

### cp

- Copies a file
- Examples
  - Copy a file to a new file or overwrites an existing one: `cp file.txt newFile.txt`
  - Copy a file to a new file to new location: `cp file.txt /dir`
  - Copy multiple files to a new file to new location: `cp file1.txt file2.txt /dir`
  - Copy all files of a pattern to new location: `cp *.txt /dir`
  - Copy the contents of folder: `cp -r /dir /other`

### file

- Describe what type a file is
- useful for checking type of file, what extension it is, if unknown
- `file file.txt` - returns details about the file

### symlinks

- A symlink (symbolic) is a type of file that points to other files or directories (folders) in Linux.
- Create symlink: `ln -s file.txt file_link.txt`
- Create symlink for dir: `ln -s dir dir_link`
- remove symlink: `rm file_link.txt`
- OVerride symlink: `ln -sf file.txt file_link.txt`


### create file or directory

#### Directories
- Create a new directory
- Examples
  - Create a new directory in current one: `mkdir newDir` 
  - Create a new directory with root permission in current one: `sudo mkdir newDir` 
  - Create a new directory in specific location: `mkdir /parent/newDir` 
  - Create a multiple new directories: `mkdir dir1 dir2` 
  - Create a multiple new directories using shortcut: `mkdir dir{1..10}` 
  - Create directory with permissions (chmod): `mkdir -m 777 dir1`
  - Create multiple directories with permissions (chmod): `(umask u=rwx,g=rwx,o=rwx && mkdir -p a/b/c)`
  - Create directoires and subdirectories, but lacks error message: `mkdir -p /parent/sub/subsub`
    - if already exists, will ignore command

#### Files

- Examples
  - empty file: `touch file.txt`
  - empty file: `> file.txt`
  - file with contents: `echo "ello world" > file.txt`
  - Create file with multiple lines: `cat > sales.txt` then type and to save `ctrl+d`
  - Append data to a file: `echo "next line" >> file.txt`
  - Open a nano or vi, and save file
  - open nano or vi with the new filename: `vi file.txt`

#### tee

-  read from standard input and write to standard output and files
- `ls -l | tee output.txt` - outputs the commands then saves to file

### deleting file or directory

- Delete a file: `rm file`
- Delete multiple files: `rm file1 file2`
- Delete multiple files of type: `rm *.pdf`
- Delete empty directories: `rm -d dir1 dir2`
- Delete filled directories: `rm -r dir1 dir2`
- Delete a file, with confirmation: `rm -i file`
- Delete a file with force: `rm -f file`
- Delete a file with logging: `rm -v file`
- 

### zipping and unzipping

- To install: `sudo apt install zip`

#### Zipping
- Zipping multiple folders: `zip -r temp.zip dir1 dir2`
- Zipping multiple files: `zip  temp.zip file1 file2`
- Zipping all files in same dir: `zip  temp.zip *`
- Zipping all files in same dir, of type: `zip -0 temp.zip *.txt`
- Zipping all files in same dir, including hidden: `zip  temp.zip .* *`
- Zipping multiple files, quiet mode: `zip -q temp.zip file1 file2`
- Zipping multiple files, password protected: `zip -e temp.zip file1 file2`
- Zipping multiple files, split into multiple zip files: `zip -s 1g temp.zip file1 file2`
- Zip files using specific compression, default is 6: `zip -9 temp.zip file1 file2`
- Add file to zipped file: `zip exisiting.zip newFile`
- Add dir to zipped file: `zip -r exisiting.zip newdir/*`

#### Unzipping

- unzip: `unzip temp.zip`
- unzip to specific location: `unzip temp.zip -d ./tmp`

### find 

- find all files in directory: `find .`
- find all files in specific directory: `find dir`
- find all files with file name extension: `find . -name=*.log`
- find all files with file name: `find . -name=file.*`
- find all files with file name with size: `find . -size +500k`
- Execute a command for all results returned by find: `find . -name=file.* -exec echo {} \` or `find . -name=file.* -exec du -h {} \`
- Precheck/dry run execute a command for all results returned by find, especially for rm: `find . -name=file.* -exec echo rm {} \`

### locate 

- searches in a snapshot of your disk, so need to run `updatedb` if adding a new file/dir
- find file, return path of file: `locate file.txt`

### clear

- https://phoenixnap.com/kb/clear-termina
- `Ctrl+L / Ctrl+Shift+K`
- `clear` - clear screen, but can scroll up for it
- `reset` -  reset command reinitializes the terminal and restores settings to default

### Bash history

- show `history`
  - search `history | grep your_search`
- clear bash history completely: `history -c`
- rerun last command `!!`
- rerun last command with sudo: `sudo !!`
- history shows key value pair, can run the key for a specific command in history: `!2003`
- rerun last nth command `!!-n`
- Reverse search
  - `ctrl + r` then start typing the command that is in history it will show, and can autocomplete with tab
  - can repeatedly press `ctrl + r` to show other matching entries in history
  - might need to use `ctrl + shift + r`
- Links
  - https://www.howtogeek.com/howto/44997/how-to-use-bash-history-to-improve-your-command-line-productivity/

### diff

- find difference between two files
  - good for comparing log files, especially large files
- `diff file1.txt file2.txt` - shows the difference between the two files
  - `diff file1.txt file2.txt --side-by-side` - show both files
  - `diff file1.txt file2.txt --color` - add colour

### cat 

- Displays the contents of a file
- concatenate files and print on the standard output
- Examples
  - `cat file.txt`
  - Display contents of multiple files: `cat file1.txt file2.txt`
  - Display contents of multiple files, after input will show next file: `cat file1.txt - file2.txt`
  - Display contents of pattern: `cat *.txt`
  - Display content of specific lines (lines 3 to 6): `cat file.txt | sed -n '3,6p'`
  - Sort line and display contents: `cat -v file.txt | sort`
  - Display line numbers: `cat -n file.txt`
  - Suppress empty lines: `cat -s file.txt`
  - Highlight end of line: `cat -E file.txt`
  - Display all tabs and nonprinting characters: `cat -A file.txt`
  - Display contents in reverse order: `tac file.txt`
  - Copy contents of one file to another: `cat file1.txt > file2.txt`
  - Append contents of one file to another: `cat file1.txt >> file2.txt`
  - Append contents of multiple files to another: `cat file1.txt file2.txt > newfile.txt`

### less

- displays the contents of a file or a command output, one page at a time
- `less file` open file in less
- `less -N file` open showing line numbers
- `less -F file` follow file
- searching in less
  - `Down arrow`, `Enter`, `e` or `j` - Move forward one line
  - `Up arrow`, `y` or `k`	- Move backward one line
  - `Space bar` or `f`	Move Forward one page
  - `b` - Move back one page
  - ```/<regex search term>``` searching forward
  - `?<regex search term>` search back
  - `n` - repeat previous search
  - `N` - repeat previous search backwards
  - `pg up` or `pg down` goes up and down through output
  - `Ng` - go to nth line
  - `shift + g` - to end of output
  - `shift + p` - to start of output
  - `shift + f` - to follow output while in less
- https://www.lifewire.com/what-to-know-less-command-4051972

### more
- allows you to quickly view a file and shows details in percentage. You can page up and down. Press ‘q‘ to quit out from the more window.
- Commands in more:
  - `enter` - scroll next line
  - `space` - next page
  - `b` - previous page
  - `z 10` - displays next 10 lines
  - `d 10` - scolls next 10 lines
  - `/ word` - search for regex
  - `q` - exit
- Examples:
  - `more -d sample.txt` - with instructions
  - `more -p sample.txt` - clear screen then prints
  - `more -c sample.txt` - keep screen, and overlaps
  - `more -s sample.txt` - squash multiple blank lines
  - `more +/word sample.txt` - searches for word/regex, use commands to navigate results
  - `more +30 sample.txt` - displays text, after 30 lines

### Head and Tail

- ```head -3 <filename>``` - show first n number of lines
- ```tail -3 <filename>``` - show last n lines
- `tail -f <filename>` - follow end of file, great for following logs as a program is run
    
### echo

- This takes the text you give it and sends it somewhere—back to the screen, to a file, or to another command. Example: echo "hello!"
- Examples
  - `echo Hello`
  - `echo "Hello World"`
  - `echo -n "Hello World"` - remove new line
  - `echo -e "Hello\tWorld\n\n"` - backslash enabled for special characters
  - `echo -E "Hello\tWorld\n\n"` - backslash disabled
  - `price="\$100 "$ echo 'The price of this book is $price"` - sub variable, Only substitutes if using double quotes

### cut 

- When you have a string with separators in it, use cut to filter out certain fields.
- echo "this, that, and the other" | cut -d, -f2 # "that"
- TBC ....................

### grep

- To find lines of text that contain a certain string, use grep.
- Example: 
  - help: `grep --help` or `man grep`
  - Specific word from a file: `grep 'root' /etc/passwd # root:x:0:0:root:/root:/bin/bash`
  - Specific word from any file in directory: `grep “string” *`
  - Show all results that dont match the specific pattern from any file in directory: `grep -v “string” *`
  - Match multiple strings, return matching line, across new lines: `grep -e ‘hello’ -e ‘fizz’’ file.txt`
  - Specific word from any file in directory, return filename: `grep -l “string” *`
  - Specific word from any file in directory, return line number: `grep -n “string” file.txt`
  - Specific word, ignoring case, from any file in directory: `grep -i “string” *`
  - Specific word from specific files in directory: `grep “string” file.txt file1.txt`
  - Specific word from specific files with extension in directory: `grep “string” *.txt`
  - Specific word from any file in specific directory: `grep -r “string” dir`
  - Specific word from any file in specific directory, excluding directory: `grep -r --exclude-dir=dir1 “string” *`
  - Specific word from any file in specific directory, excluding directories: `grep -r --exclude-dir={dir1,dir2} “string” *`
  - Specific word from any file in directory and subdirectories: `grep -r “string” *`
  - Specific word from any file in directory and subdirectories and follow symbolic links: `grep -R “string” *`
  - Specific word with wild card (match word and anything after) from any file in directory: `grep “string*” *`
  - Count number of appearance of word and location across multiple files: `grep -0 “string”   | cut -d ‘:’ -f 1 | uniq -c`
  - match across multiple lines in a file: ` grep -Pzo ‘(?s)from.*to’ file.txt`
  - match across multiple words on the same line: `grep ‘from.*to’ file.txt`
  - Show 3 lines before and after the matched word: `grep -C 3 "pattern" file.txt`
  - Show 3 lines before the matched word: `grep -B 3 "pattern" file.txt`
  - Show 3 lines After the matched word: `grep -A 3 "pattern" file.txt`
  - Show 1 line before and 2 lines after matched word: `grep -B 1 -A 2 "pattern" file.txt`
  - Show all lines before the 2nd matched word in the file: `head -n $(( $(grep -m 2 -n "sed" lorem.txt | tail -n 1 | cut -d ':' -f 1) - 1 )) lorem.txt`
  - Show all lines after the 2nd matched word, not including matched word, in the file: `tail -n $(( $(wc -l < lorem.txt | tr -d ' ') - $(grep -m 2 -n "sed" lorem.txt | tail -n 1 | cut -d ':' -f 1)  )) lorem.txt`
  - Count
    - https://www.warp.dev/terminus/grep-count

### sed
- Sed is the ultimate stream editor.
- Links
  - https://www.grymoire.com/Unix/Sed.html
  - https://www.digitalocean.com/community/tutorials/the-basics-of-using-the-sed-stream-editor-to-manipulate-text-in-linux
  - https://www.baeldung.com/linux/sed-editor
- Deleting text
  - examples...
- Printing text
  - examples...
- Substitution
  - examples...
- Search
  - Given file containing multiple lines of this form: ` Time: 2022-12-08 00:25:10.828 UTC AccountID: 1563 Env: prod [...]` and we want to find the value between AccountID and Env, we can use: `sed -e 's/.*AccountID: \(.*\)Env.*/\1/' log_file.txt`

### awk

- TBC..............

### kill a process

- kills a process
- `xkill` and click window to close
- `xlsclients` list open windoes
- `ps -A | grep -i <processName>` - to kill process
- `kill 7507` - kill a process using pid

### show processes

#### top
  - monitoring processes, mem usuage etc
  - headings
    - `PID` -  process ID, a unique positive integer that identifies a process.
    - `USER` - usernmae that maps to user id, who started the process
    - `PR` - priority of the process  
    - `NI` - nice value of process, affects the priority    
    - `VIRT` - total amount of memory consumed by a process
    - `RES` - memory consumed by the process in RAM
    - `SHR` - memory shared with other processes
    - `%MEM` - value as a percentage of the total RAM available
    - `S` - state of process
    - `%CPU` - % of cpu
    - `TIME+` -  total CPU time used by the process since it started
    - `COMMAND` - name of process
  - Commands
    - `pg up/pg dwn` - to scroll
    - `N` - sort by PID
    - `M` - sort by memory usage
    - `T` - sort by running time
    - `R` - reverse order
    - `H` - shows running threads
    - `c` - show full path of command
    - `V` - show parent child heirachy of commands
    - `U` - search process by user
    - `O` - search by filter, after applying one filter, can apply another filter on top
      - `COMMAND=blah`
      - `!COMMAND=blah`
      - `%CPU>3.0`
      - `=` to clear filters
    - `q` - to quit
  - Examples
    - `top -o %CPU` - sort by CPU

#### vmstat

- https://www.redhat.com/sysadmin/linux-commands-vmstat
    
#### du
  - monitoring disk usuage
  - `du -sh *`` summarises disk usages of the files in the current directory we use
    - `du -sh /root/test` total disk usage in folder and subfolders
  - `du -sh .[!.]* *` to include hidden files

#### df -h
  - summarises disk usage of each harddrive

#### SSD usage
  - https://www.cnet.com/how-to/find-how-how-much-longer-your-ssd-will-last/

### Watch

- running user-defined commands at regular intervals
- Example: 
  - `watch ls` - watches the command at a defualt 2s
  - `watch -n 5 ls` - watches the command at a 5s
  - `watch -d ls` - watches the command, highlights diff
  - `watch -g ls` - watches the command, exit on change
  
### view ports

- the last column shows the PID, can use to kill it off
- `netstat`
- `netsat -pant 8080` - shows info on who is listening on 8080
- `lsof -i :8080` - shows info
- TBC.............

### Permissions

- permissions
- chmod
- chown

### ssh 

-  logging into a remote machine and for executing commands on a remote machine.
-  provide secure encrypted communications between two untrusted hosts over an insecure network
- Can use without using a password, but need to setup asymmetric keys
  - https://www.ssh.com/academy/ssh/public-key-authentication
- Examples
  - `ssh usere@sample.ssh.com` - login into remote machine under user, this will ask for password
  - `ssh user@sample.ssh.com ls` - perform a command on remote machine

### Network information

- `ifconfig` - shows information regarding networks (ethernet, vpn, wifi etc)
- `ifconfig | grep inet` - to show all the ip addresses
### Curl

### Ping

- Check network connectivity
- This resolves the hostname to ip (DNS) then sends small packets to it 
- `ping www.google.com` - can use hostname or ip address

### telnet

-  connect to remote systems over a TCP/IP network
- Layer 7 protocol, similar to http
- connects to servers and network equipment over port 23
- not secure, better to use ssh
- When connecting 
  - `telnet www.google.com 80`
  - This will allow you send commands manually to a server
- To install: `yum install telnet telnet-server -y`
- https://www.digitalocean.com/community/tutorials/telnet-command-linux-unix

### scp 

- secure copy over ssh
- Example:
  - `scp -r /dir user@remotehost:~/dir` - will copy from your folder to a remote host at the home base path at dir folder

### sftp 

- secure transfer of files 
- `sftp remotehost`
- This will open interactive terminal and can transfer files
  - `mput -r /dir`

### cron
- TBC..................

### shutdown

- Use shut down the system and turn off the power. Example: shutdown -h now shuts down the system immediately. shutdown -h +5 shuts down the system after five minutes.

### environment variables

- only for session
- `echo $<name of env  variable>` - display env var if exists
- `export DATABASE_URL=localhost` - sets env var for bash session

### xargs
- TBC................

### Chmod and chown


### Alarms 

- leave {1258}
  - set alarm for current day
  
### Fun

- `printf "\n\n"; printf "Mastering\nthe\nLinux command line" | figlet -ctk; printf "\n\n"; printf '%0.1s' ' '{1..49} && printf "Han Bobo\n\n" && printf '%0.1s' ' '{1..48} && printf "blah@goole.com\n" && printf '%0.1s' ' '{1..52} && printf "@blah\n\n"`



### Others

- cut and paste
- calendar
  - shows current calendar month - `cal`
  - Shows months of a year - `cal 2023`
- Calculator
  - `bc`
  - type in expression and press enter
  - `set scale=3` will set the decimal points
  - `quit` to exit
  - instead of starting can feed it in
    - `echo 2+3 | bc`
- uptime
  - shows how long your system has been running and the number of users that are currently logged in. It also displays load average for 1,5 and 15 minutes intervals.
- w
  - displays users currently logged in and their process along with load averages. Also shows the login name, tty name, remote host, login time, idle time, JCPU, PCPU, command and processes.
- users
  -  displays currently logged in users.
- date
  - Just type date when you want to know what time it is. Example: date "+It's %l:%m%p on %A"
- who
  - simply returns user name, date, time and host information. The who command is similar to the w command. Unlike w, who doesn’t print what users are doing
- whoami
  -  prints the name of the current user. You can also use “who am i” to display the current user. If you are logged in as a root, using sudo command “whoami” returns root as current user. Use “who am i” if you want to know the exact user logged in
- sudo
- source ./bashrc
  - to run bash profile, if updating it

## makefiles


## vi 

- editor
- commands:
  - `vi` - open
  - `vi file.txt` - open file in vi
  - `i` - to insert and then can type
  - `:wq` - write and exit
  - `:q` - exit

## Links

- http://www.ee.surrey.ac.uk/Teaching/Unix/
- https://learncodethehardway.org/unix/
- https://github.com/Idnan/bash-guide
- https://github.com/enkidevs/curriculum/wiki/Linux-Topic
- https://www.freecodecamp.org/news/terminal-tips-tweets/
- https://github.com/bertjan/mastering-the-linux-command-line
  - presentation https://www.youtube.com/watch?v=qmh7Uppd3x0
- https://www.baeldung.com/linux/