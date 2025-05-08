# Week 2: Shell & Shell Scripting

## What is a Shell?

In computing, a **shell** is a user interface that provides access to the services of an operating system.

### Common Command-Line Shells:

- **Bourne Shell (sh)**

- **Bash (Bourne Again Shell)**

- **Zsh (Z Shell)**

- **KornShell (ksh)**

- **Fish (Friendly Interactive Shell)**


---

## Shell Scripting

Shell scripting is the practice of writing scripts using a shell's scripting language to automate tasks.

An expert shell script writer utilizes constructs such as:

- Loops (`for`, `while`)

- Conditional logic (`if`, `case`)

- Functions

- Stream redirection and pipelines

- Process substitution


---

## Basic Shell Scripting Commands

### Check which shell is in use:
```bash
echo $SHELL
```

### Create and run a basic Bash script:
```bash
cd Desktop/
touch hello.sh
nano hello.sh
```

**Inside `hello.sh`:**
```bash
#!/bin/bash
echo "Hello world"
```

Make it executable:
```bash
chmod +x hello.sh
./hello.sh
```

**Output:**
```
Hello world
```


---

## Variables in Shell

### Two Types of Variables:
1. **Environment Variables**
2. **User-defined Variables**

### Environment Variables Example:
```bash
echo $BASH
echo $BASH_VERSION
echo $PWD
echo $HOME
```

**Example Output:**
```
/bin/bash
4.0.12.4
/home/user/Desktop
/home/user
```

### User-defined Variables:
```bash
name="Vinitha"
echo "My name is $name"
```

**Output:**
```
My name is Vinitha
```


---

## Reading User Input
_(Section placeholder — consider adding input with `read` command)_

Week 2 - Shell and Shell Scripting
What is a Shell?
In computing, a shell is a user interface that provides access to the services of an operating system.
Common Command-Line Shells
•	Bourne Shell (sh)
•	Bash (Bourne Again Shell)
•	Zsh (Z Shell)
•	KornShell (ksh)
•	Fish (Friendly Interactive Shell)
Shell Scripting
Shell scripting is the practice of writing scripts using a shell's scripting language to automate tasks.
Constructs Used in Shell Scripting
•	Loops: for, while
•	Conditional logic: if, case
•	Functions
•	Stream redirection and pipelines
•	Process substitution
1. Getting Started with Shell Scripting
Common Terms
•	# : Sharp
•	! : Bang
•	#! : Shebang
Built-in Commands
type echo
Output: echo is a shell builtin
Check Current Shell
echo $SHELL
Create a Shell Script
•	cd Desktop/
•	touch hello.sh
•	nano hello.sh
•	#!/bin/bash
echo "hello world"
•	chmod +x hello.sh
•	./hello.sh
Output: hello world
2. Variables in Shell Scripting
Types of Variables:
•	Environment Variables
•	User-defined Variables
Examples of Environment Variables:
echo $BASH
echo $BASH_VERSION
echo $PWD
echo $HOME
Using User-defined Variables
Name='vinitha'
echo "My name is $Name"
Output: My name is vinitha
3. Working with Variables
Appending text and combining variables:
Name='vinitha'
echo "My name is ${Name}R"
Word='string'
echo "this is ${Word}ing"
echo "${Name}${Word}."
4. Special Variables and Conditionals
Displaying user info:
echo "Your user ID is ${UID}"
id -u
id -n
If Statement (Structure Placeholder)
if [ condition ]; then
  # commands
fi
5. More Concepts (Listed)
•	Special Variables
•	Pseudocode
•	Command Substitution
•	If Statements
•	Conditionals
•	Exit Statuses
•	Return Codes
•	String Test Conditionals
Manual Pages
man bash
