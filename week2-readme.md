Week:2

Shell : In computing, a shell is a user interface that provides access to the services of an operating system
Command-Line Shells:
1.	Bourne Shell (sh)
2.	Bash (Bourne Again Shell)
3.	Zsh (Z Shell)
4.	KornShell (ksh)
5.	Fish (Friendly Interactive Shell) 

2. Shell Scripting
Shell scripting is the practice of writing scripts using a shell's scripting language to automate tasks.
An expert shell script writer utilizes constructs such as:
•	Loops (for, while)
•	Conditional logic (if, case)
•	Functions
•	Stream redirection and pipelines
•	Process substitution
________________________________________

1.Getting Started with Shell Scripting: Naming, Permissions, Variables, Builtins.
# sharp
! Bang
#! Shebang
Builtins :
Type echo
O/p: echo is a shell builtins

Commands:
To check which shell is using in OS:
Echo $SHELL
How to create command bash script:
Cd desktop/
touch hello.sh
Nano hello.sh
Script:
#! /bin/bash
Echo “hello world”

Chmod +x hello.sh
./hello.sh
O/p: Hello world
Two types if variables:
1.	Environment Variables
2.	User-defined
Environment Variables:
Echo $bash
Echo $bash_version
Echo $pwd
Echo$home

O/p: /bin/bash
4.0.12.4 version
Desktop
/home/text

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
 
 
#display the uid:
Echo “your userid is ${uid}”
Uid is manual in bash
O/p: your userid is 1000
General commands manual
Command: man bash
Id -u
o/p: 1000
id -n
o/p: root
If statement:
 

O/p:
 	

 
o/p:
 

Exit Statuses, Return Codes, String Test Conditionals, More Special Variables.

 
Goal:
The goal of this exercise is to create a shell script that adds users to the same Linux system as the script is executed on.
Scenario:
Imagine that you're working as a Linux System Administrator for a fast growing company.  The latest company initiative requires you to build and deploy dozens of servers.  You're falling behind schedule and are going to miss your deadline for these new server deployments because you are constantly being interrupted by the help desk calling you to create new Linux accounts for all the people in the company who have been recruited to test out the company's newest Linux-based application.
In order to meet your deadline and keep your sanity, you decide to write a shell script that will create new user accounts.  Once you're done with the shell script you can put the help desk in charge of creating new accounts which will finally allow you to work uninterrupted and complete your server deployments on time.

 
 
O/p:
 

Random Data, Cryptographic Hash Functions, Text and String Manipulation.
Random Data:
Echo ${RANDOM}
Positional Parameters, Arguments, for Loops, Special Parameters
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
 
