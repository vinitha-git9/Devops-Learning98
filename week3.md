# Week 2: Shell Scripting and Linux Basics

## 🐚 Shell Basics

- **Shell**: User interface for accessing OS services.
- **Current Shell**: Bash (Bourne Again Shell).
- **Shell Scripting**: Automate tasks using scripting language.

### Shell Scripting Components:
- Loops (`for`, `while`)
- Conditional logic (`if`, `case`)
- Functions
- Stream redirection and pipelines
- Process substitution

---

## 🛠 Getting Started

- **Create script**: `touch hello.sh`
- **Make executable**: `chmod +x hello.sh`
- **Edit script**: `vi hello.sh`

### Shebang
```bash
#! /bin/bash
```

- `#` = Sharp  
- `!` = Bang  
- Together: Shebang

### Built-in Command Example:
```bash
type echo
# Output: echo is a shell builtin
```

- Check shell: `echo $SHELL`
- Run script: `./hello.sh`

---

## 🔧 Variables

### Environment Variables:
```bash
echo $BASH       # /bin/bash
echo $BASH_VERSION
echo $PWD        # Present working directory
echo $HOME       # Home directory
```

### User-defined Variables:
```bash
Name='vinitha'
echo "My name is $Name"
# Output: My name is vinitha
```

### Append Text:
```bash
echo "My name is ${Name}R"
```

### Combine Variables:
```bash
word='string'
echo "this is ${word}ing"
```

---

## 📥 User Input
```bash
read Name
echo "My name is $Name"
```

---

## 🧠 Conditionals and Comparisons

### Display UID and Username:
```bash
echo "Your user ID is ${UID}"
id -un   # Get username
```

### `if` Statement Syntax:
```bash
if [[ condition ]]
then
  command
fi
```

### `if-else` Example:
```bash
num=10
if [[ $num -gt 5 ]]
then
  echo "Number is greater than 5"
else
  echo "Number is less than 5"
fi
```

---

## 🔠 String Comparison Operators

| Operator | Meaning            | Example                |
|----------|--------------------|------------------------|
| ==       | Equal              | `[[ "$a" == "$b" ]]`   |
| !=       | Not equal          | `[[ "$a" != "$b" ]]`   |
| -z       | String is empty    | `[ -z "$a" ]`          |
| -n       | String not empty   | `[ -n "$a" ]`          |

---

## 📁 File Test Operators

| Operator | Tests if...        | Example               |
|----------|--------------------|------------------------|
| -e       | File exists         | `[ -e file.txt ]`     |
| -f       | Regular file        | `[ -f file.txt ]`     |
| -d       | Directory           | `[ -d dir ]`          |
| -r       | Readable            | `[ -r file.txt ]`     |
| -w       | Writable            | `[ -w file.txt ]`     |
| -x       | Executable          | `[ -x script.sh ]`    |
| -s       | File not empty      | `[ -s file.txt ]`     |

---

## 🔢 Arithmetic Operators

```bash
a=10; b=5

echo $((a + b))  # Addition
echo $((a - b))  # Subtraction
echo $((a * b))  # Multiplication
echo $((a / b))  # Division
echo $((a % b))  # Modulus
echo $((a ** b)) # Exponentiation
```

---

## 🔗 Logical Operators

| Operator | Meaning      | Example                        |
|----------|--------------|--------------------------------|
| &&       | Logical AND  | `[[ $a -gt 0 && $b -gt 0 ]]`   |
| !        | Logical NOT  | `[[ ! -f file.txt ]]`          |

---

## 📜 Script Goal

Write a script to automate user account creation, allowing Help Desk to handle user setups while the admin focuses on deployment.

---

## 🎲 Random Data

```bash
echo $RANDOM
```

---

## 📌 Positional Parameters

| Symbol  | Description             |
|---------|-------------------------|
| $0      | Script name             |
| $1, $2… | Arguments               |
| $#      | Number of arguments     |

---

## 🔁 Loops

### `for` Loop:
```bash
for fruit in apple banana cherry
do
  echo "I like $fruit"
done
```

### `while` Loop:
```bash
count=1
while [ $count -le 3 ]
do
  echo "Count is $count"
  count=$((count + 1))
done
```

---

## 🧺 Arrays

```bash
Fruits=(apple banana watermelon)
echo "${Fruits[0]}"
echo "${Fruits[@]}"
echo "${#Fruits[@]}"
```

---

## 🖥 Common Linux Commands

### 🧾 System Info
- `uname -a`
- `hostname`
- `uptime`
- `top`, `htop`
- `free -h`, `df -h`, `du -sh`
- `lscpu`, `lsblk`

### 👥 User Management
- `useradd`, `passwd`, `usermod`, `userdel`
- `groupadd`, `group`, `whoami`

### 📂 File Management
- `ls`, `cd`, `cp`, `mv`, `rm`, `mkdir`, `chmod`, `chown`

### 🌐 Network
- `ip a`, `ping`, `traceroute`, `nslookup`, `curl`, `wget`

### 📦 Package Management
- `apt update`, `apt upgrade`, `apt install`, `apt remove`

### ⚙️ Services
- `systemctl start|stop|restart|status|enable|disable`

---

## 📝 Vim Basics

### Start Vim
```bash
vim filename
```

### Insert Mode Commands
- `i` – insert
- `a` – append
- `o` – open line below

### Save & Quit
- `:w` – write
- `:q` – quit
- `:wq` or `ZZ` – save and quit
- `:q!` – force quit without saving

### Edit Commands
- `x` – delete character
- `dd` – delete line
- `yy` – copy line
- `p` – paste
- `u` – undo
- `Ctrl + r` – redo
- `ggVGy` – copy all

---

## 🧪 Example Shell Scripts

- Script to find number of lines, characters, etc.
- Script to get kernel version, memory usage, running processes, installed packages
