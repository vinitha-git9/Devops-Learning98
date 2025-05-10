
# Week 2 - Shell and Shell Scripting

## 1. Shells in Computing

A **shell** is a user interface that provides access to the services of an operating system.

### Common Command-Line Shells:

- **Bourne Shell** (`sh`)
- **Bash** (Bourne Again Shell)
- **Zsh** (Z Shell)
- **KornShell** (`ksh`)
- **Fish** (Friendly Interactive Shell)

---

## 2. Shell Scripting

Shell scripting involves writing scripts using a shell's scripting language to automate tasks.

### Key Constructs:

- Loops: `for`, `while`
- Conditionals: `if`, `case`
- Functions
- Stream redirection and pipelines
- Process substitution

---

## 3. Getting Started

### Script Basics:

- `#` - Sharp
- `!` - Bang
- `#!` - Shebang (used to specify the script interpreter)

### Built-ins:

```bash
type echo
# Output: echo is a shell builtin
```

---

## 4. Working with Shell Scripts

### Check current shell:

```bash
echo $SHELL
```

### Creating and running a shell script:

```bash
cd Desktop/
touch hello.sh
nano hello.sh
```

**Script Content:**

```bash
#!/bin/bash
echo "hello world"
```

Make it executable and run:

```bash
chmod +x hello.sh
./hello.sh
# Output: hello world
```

---

## 5. Variables in Shell

### Types:

- Environment Variables
- User-defined Variables

### Examples:

```bash
echo $BASH
# Output: /bin/bash

echo $BASH_VERSION
# Output: e.g., 4.0.12(4)

echo $PWD
# Output: current directory path

echo $HOME
# Output: /home/username
```

### Using Variables:

```bash
Name='vinitha'
echo "My name is $Name"
# Output: My name is vinitha
```

### Append Text:

```bash
echo "My name is ${Name}R"
# Output: My name is vinithaR

word='string'
echo "This is ${word}ing"
# Output: This is stringing
```

### Combine Variables:

```bash
echo "${Name}${word}."
```

---

## 6. Special Variables and Conditionals

### Display User Information:

```bash
echo "Your userid is ${UID}"  # UID is case-sensitive
id -u
# Output: 1000

id -un
# Output: username
```

### If Statement Example:

```bash
if [ "$UID" -eq 0 ]; then
  echo "You are root"
else
  echo "You are not root"
fi
```

---

## 7. Goal-Oriented Scripting

### Task:

Write a shell script to add users to the system, automating account creation to assist the help desk and improve deployment efficiency.

---

## 8. Random Data and Text Manipulation

### Generate Random Numbers:

```bash
echo $RANDOM
```

---

## 9. Arguments and Loops

### Static Input Example:

```bash
echo "First argument is $1"
echo "Total number of arguments: $#"
```

### Positional Parameters:

- `${0}` - Script name
- `${1}`, `${2}`, etc. - Arguments
- `${#}` - Number of arguments

---

## 10. Loops

### For Loop:

```bash
for i in 1 2 3
do
  echo $i
done
```

### While Loop:

```bash
while true
do
  echo "Looping..."
  sleep 1
done
```

### Shift Command:

```bash
shift
# Used to shift positional parameters to the left
```

---

## Notes

- Practice creating scripts with conditionals and loops.
- Make use of built-in variables and parameters.
- Use `man bash` to explore command documentation.
