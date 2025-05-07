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
