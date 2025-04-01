**Create SSH key**

```Shell
ssh-keygen
```

**Ask for help** - man pages - apropos - help - [explainshell.com - match command-line  
arguments to their help text  
](https://explainshell.com/)

**Check for exploits** - [Exploit Database - Exploits for  
Penetration Testers, Researchers, and Ethical Hackers  
](https://www.exploit-db.com/)

**Which kernel version is installed on the system**

```Shell
uname -r
```

If my Linux kernel version is 4.15.0-39-generic, where:

- **4** : Kernel version
- **15** : Major revision
- **0** : Minor revision
- **39** : Patch level or number
- **generic** : Linux distro/kernel specific additional  
    info  
    

Run `openvpn` in the background

```Shell
sudo openvpn --config ./academy-regular.ovpn &
```

Kill `openvpn` running in the background

```Shell
sudo killall openvpn
```

**Path to mail for current logged in user**

```Shell
cat /etc/passwd
env | grep MAIL
```

**How can I find out what shell I am using**

```Shell
printf "My current shell - %s\n" "$SHELL"echo $SHELLenv | grep SHELL
```

**Find path to files**

`Which` One of the common tools is `Which`.  
This tool returns the path to the file or link that should be executed.  
This allows us to determine if specific programs,  
like cURL, netcat, wget, python, gcc, are available on the operating  
system. Let us use it to search for Python in our interactive  
instance.  

```Shell
┌──(kjetil㉿CGAP74H09K3)-[~]└─$ which passwd
/usr/bin/passwd
```

**Find file and folders** `Find` Another  
handy tool is   
`find`. Besides the function to find files and  
folders, this tool also contains the function to filter the results. We  
can use filter parameters like the size of the file or the date. We can  
also specify if we only search for files or folders.  

```Shell
# Example "To find the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k"find / -name *.conf -type f -newermt 2020-03-03 -size +25k -size -28k 2>/dev/null
```

|   |   |
|---|---|
|Option|Description|
|`-type f`|Hereby, we define the type of the searched object. In this case,  <br>‘  <br>`f`’ stands for ‘`file`’.|
|`-name *.conf`|With ‘`-name`’, we indicate the name of the file we are  <br>looking for. The asterisk (  <br>`*`) stands for ‘all’ files with  <br>the ‘  <br>`.conf`’ extension.|
|`-user root`|This option filters all files whose owner is the root user.|
|`-size +20k`|We can then filter all the located files and specify that we only  <br>want to see the files that are larger than 20 KiB.|
|`-newermt 2020-03-03`|With this option, we set the date. Only files newer than the  <br>specified date will be presented.|
|`-exec ls -al {} \;`|This option executes the specified command, using the curly brackets  <br>as placeholders for each result. The backslash escapes the next  <br>character from being interpreted by the shell because otherwise, the  <br>semicolon would terminate the command and not reach the  <br>redirection.|
|`2>/dev/null`|This is a `STDERR` redirection to the  <br>‘  <br>`null device`’, which we will come back to in the next  <br>section. This redirection ensures that no errors are displayed in the  <br>terminal. This redirection must   <br>`not` be an option of the  <br>‘find’ command.|

`Locate` It will take much time to search through the  
whole system for our files and directories to perform many different  
searches. The command   
`locate` offers us a quicker way to  
search through the system. In contrast to  
the   
`find` command, `locate` works with a local  
database that contains all information about existing files and folders.  
We can update this database with the following command.  

```Shell
┌──(kjetil㉿CGAP74H09K3)-[~]└─$ sudo updatedb
```

If we now search for all files with the “`.conf`”  
extension, you will find that this search produces results much faster  
than using   
`find`.

```Shell
┌──(kjetil㉿CGAP74H09K3)-[~]└─$ locate *conf
/etc/adduser.conf/etc/ca-certificates.conf/etc/debconf.conf/etc/deluser.conf/etc/e2scrub.conf/etc/gai.conf/etc/host.conf
```

However, this tool does not have as many filter options that we can  
use. So it is always worth considering whether we can use  
the   
`locate` command or instead use  
the   
`find` command. It always depends on what we are looking  
for.  

**Search in man pages** | Option | Description | |  
————–|——————-| |  
`\` | Type search word of the tool you want  
to learn more of  

**Command Cheat Sheet**

|   |   |
|---|---|
|**Command**|**Description**|
|`man <tool>`|Opens man pages for the specified tool.|
|`<tool> -h`|Prints the help page of the tool.|
|`apropos <keyword>`|Searches through man pages’ descriptions for instances of a given  <br>keyword.|
|`cat`|Concatenate and print files.|
|`whoami`|Displays current username.|
|`id`|Returns users identity.|
|`hostname`|Sets or prints the name of the current host system.|
|`uname`|Prints operating system name.|
|`pwd`|Returns working directory name.|
|`ifconfig`|The `ifconfig` utility is used to assign or view an  <br>address to a network interface and/or configure network interface  <br>parameters.|
|`ip`|Ip is a utility to show or manipulate routing, network devices,  <br>interfaces, and tunnels.|
|`netstat`|Shows network status.|
|`ss`|Another utility to investigate sockets.|
|`ps`|Shows process status.|
|`who`|Displays who is logged in.|
|`env`|Prints environment or sets and executes a command.|
|`lsblk`|Lists block devices.|
|`lsusb`|Lists USB devices.|
|`lsof`|Lists opened files.|
|`lspci`|Lists PCI devices.|
|`sudo`|Execute command as a different user.|
|`su`|The `su` utility requests appropriate user credentials  <br>via PAM and switches to that user ID (the default user is the  <br>superuser).  A shell is then executed.|
|`useradd`|Creates a new user or update default new user information.|
|`userdel`|Deletes a user account and related files.|
|`usermod`|Modifies a user account.|
|`addgroup`|Adds a group to the system.|
|`delgroup`|Removes a group from the system.|
|`passwd`|Changes user password.|
|`dpkg`|Install, remove and configure Debian-based packages.|
|`apt`|High-level package management command-line utility.|
|`aptitude`|Alternative to `apt`.|
|`snap`|Install, remove and configure snap packages.|
|`gem`|Standard package manager for Ruby.|
|`pip`|Standard package manager for Python.|
|`git`|Revision control system command-line utility.|
|`systemctl`|Command-line based service and systemd control manager.|
|`ps`|Prints a snapshot of the current processes.|
|`journalctl`|Query the systemd journal.|
|`kill`|Sends a signal to a process.|
|`bg`|Puts a process into background.|
|`jobs`|Lists all processes that are running in the background.|
|`fg`|Puts a process into the foreground.|
|`curl`|Command-line utility to transfer data from or to a server.|
|`wget`|An alternative to `curl` that downloads files from FTP or  <br>HTTP(s) server.|
|`python3 -m http.server`|Starts a Python3 web server on TCP port 8000.|
|`ls`|Lists directory contents.|
|`cd`|Changes the directory.|
|`clear`|Clears the terminal.|
|`touch`|Creates an empty file.|
|`mkdir`|Creates a directory.|
|`tree`|Lists the contents of a directory recursively.|
|`mv`|Move or rename files or directories.|
|`cp`|Copy files or directories.|
|`nano`|Terminal based text editor.|
|`which`|Returns the path to a file or link.|
|`find`|Searches for files in a directory hierarchy.|
|`updatedb`|Updates the locale database for existing contents on the  <br>system.|
|`locate`|Uses the locale database to find contents on the system.|
|`more`|Pager that is used to read STDOUT or files.|
|`less`|An alternative to `more` with more features.|
|`head`|Prints the first ten lines of STDOUT or a file.|
|`tail`|Prints the last ten lines of STDOUT or a file.|
|`sort`|Sorts the contents of STDOUT or a file.|
|`grep`|Searches for specific results that contain given patterns.|
|`cut`|Removes sections from each line of files.|
|`tr`|Replaces certain characters.|
|`column`|Command-line based utility that formats its input into multiple  <br>columns.|
|`awk`|Pattern scanning and processing language.|
|`sed`|A stream editor for filtering and transforming text.|
|`wc`|Prints newline, word, and byte counts for a given input.|
|`chmod`|Changes permission of a file or directory.|
|`chown`|Changes the owner and group of a file or directory.|