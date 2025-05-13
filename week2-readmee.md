# Shell Scripting Notes (Week 2)

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

== : equal

!= : not equal

-z : string is empty

-n : string is not empty

Common file test operators:

-f : regular file exists

-d : directory exists

-e : file or directory exists

-r : readable

-w : writable

-x : executable

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

Comparison Operators (Numbers)

3. Comparison Operators (Strings)

Logical Operators

🔹 5. File Test Operators

🔹 6. Assignment Operators

Exit Statuses, Return Codes, String Test Conditionals, More Special Variables.

Goal:

The goal of this exercise is to create a shell script that adds users to the same Linux system as the script is executed on.

Scenario:

Imagine that you're working as a Linux System Administrator for a fast growing company.  The latest company initiative requires you to build and deploy dozens of servers.  You're falling behind schedule and are going to miss your deadline for these new server deployments because you are constantly being interrupted by the help desk calling you to create new Linux accounts for all the people in the company who have been recruited to test out the company's newest Linux-based application.

In order to meet your deadline and keep your sanity, you decide to write a shell script that will create new user accounts.  Once you're done with the shell script you can put the help desk in charge of creating new accounts which will finally allow you to work uninterrupted and complete your server deployments on time.

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

Basics of Vim editor:

🚀 Starting Vim : vim filename

Basic Vim Workflow: Other insert commands:

I → Insert at beginning of line

a → Append after cursor

o → Open new line below and insert

2. Exit Insert Mode

Press Esc

3. Save and Quit

ggVGy                Copy all

1. Shell script to find no of line, characters and other functions

O/P:

Shell script to find kernal version, memory usage, running process, installed packages

O/P:

