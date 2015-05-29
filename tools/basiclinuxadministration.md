***Top 3 Most Important Things***

man <command> will give you the manual for a specific command 

If you hit tab, it will auto-complete commands 

Everything is case sensitive! 

[Very Beginner Linux Users Guide](http://www.ee.surrey.ac.uk/Teaching/Unix)

=User Administration=
If a file called /etc/nologin exists, no users can login.  Any text in said file will be displayed 

==Adding a User==
The useradd command will add a user, it is located in /usr/sbin/
You can use the -g switch to add that user to a group as well, for multiple groups use -G

==Adding a group==
addgroup

==Deleting a user==
userdel <username>

Using the -r switch will also remove their home directory

==Who==
This command tells you who is logged in and what terminal they are on 

who -a adds a whole bunch of other userful info an can tell you where users are connected from 

Alias is w 

==Sudoers==
Tells what users have permissions to change their user to the root user upon request with username/password using the sudo command

Users can also change users without logging out using the "su" command along with the name of the user they want login with. 

==Password File==
This file listed in /etc/passwd should never actually list passwords, but it does have a list of users and account info.

Each user has his own line of info separated with colons:
* username (1-32 characters)
* password (x means password is in /etc/shadow)
* User ID or UID
** Each user will get a user id or UID.  That number will tell you what type of user they are.
** 0 root the administrator account
** 1-999 Service accounts and System administration
** 1000+ User accounts
* Group User ID GUID
* User info
* home directory
* shell

The actual password info is stored in /etc/shadow encrypted

Each user has their own line of info separated by colons:
* username
* password
** If the beginning of the password field starts with "$id$Salt$hash" the password was stored with something besides DES (DES is easy to break)
** "$1$" represents MD5
** "$2$" represents Blowfish
** "$5$" represents SHA-256
** "$6$" represents SHA-512
** "NP" or "!" or null means the account has no password
** "LK" or "*" means the account is locked"
** "!!" means the password has expired
* Time since last password was changed (in epoch time or days since Jan. 1st 1970)
* Minimum Number of days between password changes
* Maximum Number of days the password is valid
* Warn is the number of days before a users password expires that he is warned 
* Inactive number of days after password expires before that account is disabled
* Expire - when the user can no longer login (in epoch time)

Some New systems are using SHA-512 currently. This is set in /etc/pam.d/common-password 

==Logging in without a password==
If you are able to reboot the computer into single user mode, it will bypass password authentication allowing you to recover a system if you forgot or lose your root password.

=File Info=

Seen via the "ls" command with the "-l" switch 
The lines after will give you meta-data for each file like the following:
  -rw-r--r-- 1 root root 2021 2012-06-21 23:23 Keys.txt
  -rwxr-xr-x 1 root root   82 2012-04-08 10:16 urlcheck

The first 10 values deal with the file permissions, the next value represents the number of files represented by that file/directory (if its a directory it would include the number of items in it), the file owner, the group the file is owned by, the size of the file in bytes, and the date & time the file was last modified then the name of the file

The first character will give you some details about the file: 
  d for directory
  - for a regular file
  l for a symbolic link
  s Unix Domain Socket
  p named pipe
  c character device file
  b block device file

==Hidden Files==
Files are hidden by having the first character as "." like ".temp" as a file name

When using the "ls" command, you can use a "-a" switch to show hidden files as well such as "ls -a"

==Permissions==
===Basic File Permissions===

The next 9 characters are permission information in 3 groupings of 3 permission 
There are 3 different groupings is linux file permissions: User (u), Group (g), Other (o)
The three permission types are: Read (r), Write (w), and Execute (x) 

You change permissions using the "chmod" command like the following examples
You can grant execute permission for the User or file owner like this: 
  chmod u+x Keys.txt

You can remove execute permissions from the User or file owner like this: 
  chmod u-x Keys.txt

You can set all groupings with only read permission like this:
  chmod a=r Keys.txt

You can also set permissions using 3 digital octal numbers:  
  4 read (r)
  2 write (w)
  1 execute (x)
  0 no permission (-)

So to set the file owner with all 3 permissions, group with Read and Write Permissions and Other with just read permissions, you would use the following command:
  chmod 764 Keys.txt

===Sticky Bit===
Allows  folder or file to ignore write/execute permissions except for the file owner

===SetUID or SetGUID===
A file which allows you to change what group you are in or what user you are

===Symlinks===
Allows linking the same file in different places 

==File Attributes==
Some files can be set with special attributes like immutable (can't be changed until the flag is removed) using the "chattr" command. 

To set different attributes, you can "+", "-" or "=" 

File Attribute types include:
  i immutable (can't be changed)
  u undeletable 
  c compressed
  a append only (can add, but not edit/remove)

There are more, but those are the most important ones. 

===Immutable===
So to set the Keys.txt file as immutable, you would type:
  chattr +i Keys.txt

To get a list of File Attributes, you can use the "lsattr" command 

To get a list of all immutable files
  find / -type f \( -perm -4000 -o -perm -2000 \) -exec ls -lah {} \; 2>/dev/null
  from Justin Wray's Defensive Tools for the Blind ([http://sourceforge.net/p/dtftb/code/2/tree/trunk/linux/find_setid.sh])

===Image Metadata===
Make friends with "exiftool" 

=Shells=
There are many different types of shells available for linux and it is important to understand what they are, especially when setting what users default to which shells. 

  /bin/bash is the default for users
  /bin/false is for users that don't know a shell like the spool service
  /bin/sh predecessor to bash

There are many other shells, but these are the most common 

Shell configurations vary depending on the shell. /etc/skel shows the default when a new user is created
/etc/profile and the .profile file of the user are run on login in sh, ksh, bash, and zsh 

The individual users .profile (hidden) file is in their home directory 

For bash, their home directory also contains and runs the following files on login:
  .bash_profile
  .bash_login

Bash reads the .bash_logout file from the users home directory when they logout 

Bash reads the .bashrc file when a shell is created that is not a login shell but is interactive 

The easiest way to kill a shell is to use the "fuser -k" command like this:
  fuser -k pts/2

The example above will kill the shell of user on pts/2 

"env" holds temporary environment variables, be careful if you change any of these, you shell seem broken 
As long as the user is set properly, all commands are stored in the users home directory in .bash_history 
Bash History is an environment variable that can be changed

==Home Folders==
Each user is usually given a home folder as well as one for root.  User home folders are in /home/<username> while root is typically /root/ 

You can replace the path to a home folder by using "~/" then the folder name, that will put you in the home folder for your user.

=Processes=
The "ps" command gives you a list of all current processes.  I personally like to use it with the following switches "ps auxwww" that gives far more information then the base command.  It includes all the processes the full command used when starting a process,
and much more.  The "ps" command gives you whats running on your TTY.

It is important to find the Process ID (PID) from "ps" if you need to end a process 

==Kill==
To kill a process, use the kill command with a certain signal to decide how the process dies.
  kill -hup restarts a process (loading a new config)
  kill -9 PID means kill it now, don't care what happens to it, just make it die (example: "kill -9 1443" would kill process 1443)
  kill PID ends a task somewhat gracefully

==List Open Files==
The "lsof" command gives you a list of all open files and connections.  I suggest using it with the switches "lsof -nPi" 

The -i switch will add connections and you can limit that in various ways if you want 
The -n option does not resolve hostnames (runs faster and won't alert attacker 
The -P option does not resolve port names (runs faster and less confusing as a port number doesn't guarantee the service using it)  

==List Connections==
The "netstat" command gives you a list of all connections.  I suggest using it with the switches "netstat -anop"

The -a switch gives you all connections
The -n switch shows using numerical addresses instead of resolving hostnames (runs faster and won't alert attacker 
The -o switch shows timers
The -p switch shows the Program ID and name to which the socket belongs

==Top==
The "top" command shows you what is running, priority level and what resources everything is using.  The "htop" command is a better version of the same tool.

==Monitor Traffic==
===iptraf===
Awesome Tool that shows you where you traffic is going

=Logs=
Know them, love them

Most are in /var/log

==Scheduled Tasks==
Cron

==Background and Foreground==

=Packages and Package Managers=
==Apt-Get==
==DPKG==
==RPM==
==Other==
Immerge for gentoo (might be spelled wrong, but its gentoo...)
Pacman for Arch 

=Services=
Most config files for a service are in /etc/  
Configuration files can lead to many vulnerabilities 
If it isn't necessary, its probably better to turn it off 

==SMB==
==Apache==
==PHP==
php.ini is the config file, harden it

==SSHd==
The daemon allowing remote login via Secure Shell (or SSH).  

Instead of using passwords, this can be configured to use keys.  These keys are typically stored in the users home directory in a subdirectory ".ssh"

=Drives=
mount command
stored in /etc/fstab

=Networking=
ifconfig - same as windows varient ipconfig except better/more powerful

=Firewall=
==IPTables==
==PF==

=Filtering Commands=
[http://www.theunixschool.com/p/awk-sed.html AWK and SED Guide] 
Pipe - take the output of the command before the pipe and shove into standard in on the next command. 

[Tools](../tools.md)
