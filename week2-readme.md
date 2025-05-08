---
title: "Week 2 - Shell and Shell Scripting"
output: html_document
---

# What is a Shell?

In computing, a **shell** is a user interface that provides access to the services of an operating system.

## Common Command-Line Shells

- Bourne Shell (`sh`)
- Bash (Bourne Again Shell)
- Zsh (Z Shell)
- KornShell (`ksh`)
- Fish (Friendly Interactive Shell)

# Shell Scripting

Shell scripting is the practice of writing scripts using a shell's scripting language to automate tasks.

## Constructs Used in Shell Scripting

- Loops: `for`, `while`
- Conditional logic: `if`, `case`
- Functions
- Stream redirection and pipelines
- Process substitution

# Getting Started with Shell Scripting

### Common Terms

- `#` : Sharp
- `!` : Bang
- `#!` : Shebang

### Built-in Commands

```bash
type echo
# Output: echo is a shell builtin
```

### Check Current Shell

```bash
echo $SHELL
```

### Create a Shell Script

```bash
cd Desktop/
touch hello.sh
nano hello.sh
```

**hello.sh**
```bash
#!/bin/bash
echo "hello world"
```

Make the script executable and run it:

```bash
chmod +x hello.sh
./hello.sh
# Output: hello world
```

# Variables in Shell Scripting

### Types of Variables

- Environment Variables
- User-defined Variables

### Examples of Environment Variables

```bash
echo $BASH
echo $BASH_VERSION
echo $PWD
echo $HOME
```

### Using User-defined Variables

```bash
Name='vinitha'
echo "My name is $Name"
# Output: My name is vinitha
```

# Working with Variables

```bash
Name='vinitha'
echo "My name is ${Name}R"

Word='string'
echo "this is ${Word}ing"
echo "${Name}${Word}."
```

# Special Variables and Conditionals

```bash
echo "Your user ID is ${UID}"
id -u
id -n
```

# If Statement (Structure Placeholder)

```bash
if [ condition ]; then
  # commands
fi
```

# More Concepts

- Special Variables
- Pseudocode
- Command Substitution
- If Statements
- Conditionals
- Exit Statuses
- Return Codes
- String Test Conditionals

# Manual Pages

```bash
man bash
```
