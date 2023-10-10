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

### Bash history
-  show `history`
-  search `history | grep your_search`
- clear bash history completely: `history -c`
- rerun last command `!!`
- rerun last nth command `!!-n`
- https://www.howtogeek.com/howto/44997/how-to-use-bash-history-to-improve-your-command-line-productivity/#:~:text=View%20Your%20Bash%20History&text=The%20command%20with%20a%20%E2%80%9C1,number%20is%20the%20most%20recent.&text=You%20can%20do%20anything%20you,to%20search%20your%20command%20history.

### Others

- ls
  - flags -al
- pwd
  - Where am I? Linux can be unforgiving, particularly when you delete something. Make sure you know where you are before you issue your commands.
- cd
  - multiple folders
  - to root
- copy ```cp```
  - Copy file from source to destination preserving same mode
- move ```mv```
  - used to rename
    - mv text new
  - to move files with the command line
- ```.```
- cat
  - combining text
  - showingfile
  - To display the contents of a text file, just type cat myfile.
- less
  - allows you to quickly view a file. You can page up and down. Press ‘q‘ to quit from the less window
  - searching in less
    - ```head -3 <filename>```
      - show first n number of lines
    - ```tail -3 <filename>```
      - show last n lines
    - '''tail -f <filename>
      - follow end of file, great for following logs as a program is run
    - ```/<regex search term>``` searching within less
  - https://www.lifewire.com/what-to-know-less-command-4051972
- more
  - allows you to quickly view a file and shows details in percentage. You can page up and down. Press ‘q‘ to quit out from the more window.
- echo
  - This takes the text you give it and sends it somewhere—back to the screen, to a file, or to another command. Example: echo "hello!"
- grep
  - To find lines of text that contain a certain string, use grep.
  - Example: grep 'root' /etc/passwd # root:x:0:0:root:/root:/bin/bash
- find
  - It does what it says, and it’s good at it. Use it to locate files by path, size, date, owner and a bunch of other useful filters. Example: find . -type f -mtime -1h # List files in this directory modified in the past hour.
- sed
  - Use sed to find and change a substring in a piece of text. Example: echo "this, that, and the other" | sed 's/that/those/' # "this, those, and the other"
- cut
  - When you have a string with separators in it, use cut to filter out certain fields.
  - echo "this, that, and the other" | cut -d, -f2 # "that"
- create file
- shutdown
  - Use shut down the system and turn off the power. Example: shutdown -h now shuts down the system immediately. shutdown -h +5 shuts down the system after five minutes.
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
  - This command removes files, not directories. rm file.txt will remove the file named "file.txt" as long as it exists and is in the current directory.
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
    - `du -sh /root/test` total disk usage in folder and subfolders
  - `du -sh .[!.]* *` to include hidden files
- df -h
  - summarises disk usage of each harddrive
- SSD usage
  - https://www.cnet.com/how-to/find-how-how-much-longer-your-ssd-will-last/
- source ./bashrc
  - to run bash profile, if updating it
- crontab
  - lists scheduled jobs for current user with crontab command and -l option.
- count number of files
  -  ls -1 | wc -l
- leave {1258}
  - set alarm for current day

## symlink

- https://www.freecodecamp.org/news/symlink-tutorial-in-linux-how-to-create-and-remove-a-symbolic-link/

## Permissions

## makefiles

## Links

- http://www.ee.surrey.ac.uk/Teaching/Unix/
- https://learncodethehardway.org/unix/
- https://github.com/Idnan/bash-guide
- https://github.com/enkidevs/curriculum/wiki/Linux-Topic
- https://www.freecodecamp.org/news/terminal-tips-tweets/
- https://github.com/bertjan/mastering-the-linux-command-line
  - presentation https://www.youtube.com/watch?v=qmh7Uppd3x0
