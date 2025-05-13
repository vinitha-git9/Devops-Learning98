Week:2

Shell : user interface that provides access to the services of an operating system
Current shell : Bash (Bourne Again Shell
Shell scripting :writing scripts using a shell's scripting language to automate tasks.
              Loops (for, while) ,Conditional logic (if, case) ,Functions, Stream redirection and pipelines, Process substitution
Getting Started with Shell Scripting: Naming, Permissions, Variables, Builtins.
Naming:  touch hello.sh
Permissions: chmod +x hello.sh
How to open shell script: vi hello.sh
#! /bin/bash 
# sharp
! Bang
#! Shebang
Builtins : Type echo
O/p: echo is a shell builtins
To check which shell is using in OS: Echo $SHELL
How to run the script:  ./ hello.sh
Two types if variables:
Environment Variables
          Command	O/P
Echo $bash	/bin/bash
Echo $bash_version	4.0.2.5
Echo $pwd	Desktop
Echo $home	/home/text

User-defined varaibles:
How to use variables:
Name=’vinitha’
Echo “my name is $Name”
o/p:  my name is vinitha
Read User Input:
 
 
 
Append text to varaiable:
Name ‘vinitha’
Echo “my name is ${Name}R”
0r
Word ‘string’
Echo “this is ${word}ing”
Combine two variable:
Echo “${name}${word}.”
Special Variables, Pseudocode, Command Substitution, if Statement, Conditionals.
#display the userid and username of the executing user:
#display if the user is root user or not.
UID-to find user id
id -un (used to find the username of the user)
$(...) runs id -un and replaces it with the result.
 
 
#display the uid:
Echo “your userid is ${UID}”
Uid is manual in bash
O/p: your userid is 1000
General commands manual
Command: man bash
Id -u
o/p: 1000
id -n
o/p: root
If statement:
Syntax:
If  [[ condition ]]
Then
Command
Fi
if-else Condition

num=10
if [[  ${num}  -gt  5 ]]
then 
echo “Number is greater than 5”
else
echo “Number is lesser than 5”
fi
 

O/p:
 	

 
o/p:
 
🔹 4. String Comparison:
Operators:
•	== : equal
•	!= : not equal
•	-z : string is empty
•	-n : string is not empty
Common file test operators:
•	-f : regular file exists
•	-d : directory exists
•	-e : file or directory exists
•	-r : readable
•	-w : writable
•	-x : executable
5. File Conditions
Example:
File=”file.txt”
If [[  -f “file.txt” ]]
Then
Echo “file exist”
Operators:
-f file exsit
-d directory exist
-e file or directory exist
-r reaaable
-w writable
-x executable
Operator	Description	Example
+	Addition	((a+b))
-	Subtraction	((a - b))
*	Multiplication	((a * b))
/	Division	((a / b))
%	Modulus (remainder)	((a % b))
**	Exponentiation	((a ** 
b))
++	Increment	((a++)) or ((++a))
--	Decrement	((a--)) or ((--a))
		
Comparison Operators (Numbers)
Operator	Meaning	Example
-eq	Equal	[ $a -eq $b ]
-ne	Not equal	[ $a -ne $b ]
-gt	Greater than	[ $a -gt $b ]
-lt	Less than	[ $a -lt $b ]
-ge	Greater or equal	[ $a -ge $b ]
-le	Less or equal	[ $a -le $b ]
3. Comparison Operators (Strings)

Operator	Meaning	Example
= or ==	Equal	[[ "$a" == "$b" ]]
!=	Not equal	[[ "$a" != "$b" ]]
-z	Is empty string	[ -z "$a" ]
-n	Is not empty	[ -n "$a" ]

Logical Operators

Operator	Meaning	Example
&&	Logical AND	[[ $a -gt 0 && $b -gt 0 ]]
`		`
!	Logical NOT	[[ ! $a -eq 0 ]]

🔹 5. File Test Operators
Operator	Tests if...	Example
-e	File exists	[ -e file.txt ]
-f	Regular file	[ -f file.txt ]
-d	Directory	[ -d dir_name ]
-r	Readable	[ -r file.txt ]
-w	Writable	[ -w file.txt ]
-x	Executable	[ -x script.sh ]
-s	File not empty	[ -s file.txt ]
🔹 6. Assignment Operators
Operator	Meaning	Example
=	Assign value	a=10
+=	Add and assign	((a += 5))
-=	Subtract and assign	((a -= 5))
*=	Multiply and assign	((a *= 2))

Exit Statuses, Return Codes, String Test Conditionals, More Special Variables.

 
Goal:
The goal of this exercise is to create a shell script that adds users to the same Linux system as the script is executed on.
Scenario:
Imagine that you're working as a Linux System Administrator for a fast growing company.  The latest company initiative requires you to build and deploy dozens of servers.  You're falling behind schedule and are going to miss your deadline for these new server deployments because you are constantly being interrupted by the help desk calling you to create new Linux accounts for all the people in the company who have been recruited to test out the company's newest Linux-based application.
In order to meet your deadline and keep your sanity, you decide to write a shell script that will create new user accounts.  Once you're done with the shell script you can put the help desk in charge of creating new accounts which will finally allow you to work uninterrupted and complete your server deployments on time.

323. 
 
O/p:
 

Random Data, Cryptographic Hash Functions, Text and String Manipulation.
lRandom Data:
Echo ${RANDOM}
Positional Parameters, Arguments, for Loops, Special Parameters
It's a key part of conditional scripting:
if [ $? -eq 0 ]; then
  echo "Command succeeded"
else
  echo "Command failed"
fi

Arguments in Shell:
Static input:
 
o/p
 

Positional Parameters

${0} fisrt argument
${1} second argument
${2} third argument
………………………… ${#} -TOTAL NO.OF ARGUMENT

 
o/p:


 
Dynamic Input:

 
O/P:
 

For loop:
 
o/p:
 
The while Loop, Infinite Loops, Shifting, Sleeping
While loop:
 
 
True: 
Do nothing return the exit comment as 0
Sleep:
 

SHIFT:
 
o/p:


 
For Loop:
for var in item1 item2 item3
do
  command(s)
done
Example:
for fruit in apple banana cherry
do
  echo "I like $fruit"
done
Output:
I like apple
I like banana
I like cherry

🔁 2. While Loop

while [ condition ]
do
  command(s)
done
Example:
count=1
while [ $count -le 3 ]
do
  echo "Count is $count"
  count=$((count + 1))
done
o/p:
Count is 1
Count is 2
Count is 3

Arrays: store multiple values in a single variable
Basic Array Syntax:
Declaring an Array:  Fruits=(apple,banana,watermelon)
Accessing Elements: echo “${Fruits[0]}”
All Elements: echo “${Fruits[@]}”
Array Length: echo “${#Fruits[@]}”

 




 
 


Operator	Description	Example
+	Addition	echo $((a+b))
-	Subtraction	echo $((a-b))
*	Multiplication	echo $((a*b))
/	Division	echo $((a/b))
%	Modulus (remainder)	echo $ ((a%b))
**	Exponentiation	echo $((a **))
Operator	Description	Example
-eq	Equal to	[[ $a -eq $b ]]
-ne	Not equal to	[[ $a -ne $b ]]
-gt	Greater than	[[ $a -gt $b ]]
-lt	Less than	[[ $a -lt $b ]]
-ge	Greater or equal	[[ $a - ge $b ]]
-le	Less or equal	[[ $a - le $b ]]
Operator	Description	 
=	Equal	[[ $a = $b ]]
!=	Not equal	[[ $a != $b ]]
<	Less than (alphabetical)	[[ $a < $b ]]
>	Greater than (alphabetical)	[[ $a >$b ]]
-z	String is null (empty)	[[ -z $b ]]
-n	String is not empty	[[ -n $b ]]
Operator	Description	 
-e	File exists	[[ -e "file.txt" ]]
-f	Regular file	[[ -f "file.txt" ]]
-d	Directory	[[ -d "file.txt" ]]
-r	Readable	[[ -r "file.txt" ]]
-w	Writable	[[ -w "file.txt" ]]
-x	Executable	[[ -x "file.txt" ]]
-s	Not empty	[[ -s "file.txt" ]]
Operator	Description	 
&&	Logical AND	[[ $a -gt 0 && $b -gt 0 ]]
`	 	 
!	Logical NOT	[[ ! -f "file.txt" ]]
 	 	 
 	 	 
 	 	 
 	 	 
 	 	 

Command	Description
uname -a	Show system info
hostname	Show or set system hostname
uptime	Show how long the system has been running
top/htop	Display running processes (interactive)
vmstat	Report memory, CPU, and IO usage
free -h	Show memory usage
df -h	Show disk space usage
du -sh	Show folder size
lscpu/lsblk	Show CPU and block device info
who iam	Show who is logged in
Command	Description
useradd	Add a new user
passwd (user)	Set or change user password
usermod	Modify user account
userdel	Delete a user
groupdel	Add a new group
group [user]	Show user’s group memberships
Command	Description
ls -l	List files with details
cd	Change directory
cp	Copy file or directory
mv	Move or rename
rm	Delete file
mkdir	Create new directory
filename -m	Search for files
chmod	Change permissions
chown	Change owner
Command	Description
apt update	Update package list
apt upgrade	Upgrade all packages
apt nstall	Install a package
apt remove	Remove a package
Command	Description
ip a	Show network interfaces
ping hostname	Check network connectivity
 	Show listening ports
 	Show sockets
traceroute	Trace route to host
nslookup	DNS lookup
curl url	HTTP request
wget url	Download file from URL
Command	Description
ps aux	Show all running processes
kill [pid]	Kill a process
	
killall [name]	Kill processes by name
 	Set process priority
Command	Description
chmod	Change file permissions
chown	Change ownership
sudo	Run command as superuser
ufw	Firewall management (Ubuntu)
iptables	Advanced firewall rules
 	Description
systemctl start	Start a service
systemctl stop	Stop a service
systemctl restart	Restart a service
systemctl status	Get service status
systemctl enable	Enable service on boot
systemctl disable	Disable service from boot

Description	Command
List directory contents	Ls
Long listing format	ls -l
Change directory	cd [dir]
Show current directory	Pwd
Create directory	mkdir [dir]
Remove empty directory	rmdir [dir]
Remove file	rm [file]
Remove directory recursively	rm -r [dir]
Copy file or directory	cp source dest
Move or rename file/directory	mv source dest
Create empty file	touch file
Display file contents	cat file
View file page-by-page	less / more
Search for files	find /path -name filename
Description	Command
Show free disk space (human-readable)	df -h
Show total size of a directory	du -sh [dir]
List files with sizes	ls -lh
Show file details	stat file
Description	Command
Show current user	whoami
Add new user	adduser username
Change user password	passwd username
Switch to another user	su - username
Run command as root	sudo command
Change permissions	chmod 755 file
Change owner of file	chown user:group file
Description	Command
Create tar archive	tar -cvf archive.tar dir
Extract tar archive	tar -xvf archive.tar
Compress a file	gzip file
Decompress a .gz file	gunzip file.gz
Zip files	zip file.zip file1
Unzip files	unzip file.zip
Description	Command
List all running processes	ps aux
Interactive process viewer	top / htop
Kill process by PID	kill PID
Kill process by name	killall name
Show how long system has been running	uptime
Shutdown immediately	shutdown -h now
Restart system	reboot
Description	Command
Show IP address & network interfaces	ip a
Ping a host	ping host
Trace route to a host	traceroute host
Show open ports	netstat -tuln
Fetch a web page	curl url
Download file from URL	wget url
Copy file from remote machine (SSH)	scp user@host:/file .
Connect to remote machine	ssh user@host
Description	Command
Refresh package list	apt update
Upgrade packages	apt upgrade
Install package	apt install packagename
Remove package	apt remove packagename
Description	Command
Simple command-line text editor	nano file
Advanced text editor	vim file
View contents	cat file

Basics of Vim editor:
🚀 Starting Vim : vim filename
Basic Vim Workflow: Other insert commands:
•	I → Insert at beginning of line
•	a → Append after cursor
•	o → Open new line below and insert

2. Exit Insert Mode
Press Esc
3. Save and Quit
Command	Action
:w	Save (write) the file
:q	Quit
:wq or ZZ	Save and quit
:q!	Quit without saving

Command	Description
x	Delete character under cursor
dd	Delete (cut) current line
yy	Copy (yank) current line
p	Paste
u	Undo
Ctrl + r	Redo
  ggVGy                Copy all




1. Shell script to find no of line, characters and other functions

 

O/P:
 

 
 


Shell script to find kernal version, memory usage, running process, installed packages
 
O/P:

 
