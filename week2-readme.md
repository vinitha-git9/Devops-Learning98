
# Week 2: Shell Scripting Basics

## 🐚 Shell Overview

- **Shell**: Interface to access OS services.
- **Current Shell**: `bash` (Bourne Again Shell)
- **Shell Scripting**: Automating tasks using shell scripting language.

Key features:
- Loops: `for`, `while`
- Conditionals: `if`, `case`
- Functions
- Stream redirection & pipelines
- Process substitution

---

## 🔧 Getting Started

### Naming and Permissions

```bash
touch hello.sh         # Create script
chmod +x hello.sh      # Make executable
vi hello.sh            # Edit script
```

### Shebang

```bash
#! /bin/bash
# '!' = Bang, '#' = Sharp → Together: Shebang
```

### Built-in Commands

```bash
type echo      # echo is a shell builtin
echo $SHELL    # Show current shell
```

### Running Script

```bash
./hello.sh
```

---

## 🧩 Variables

### Types

- **Environment Variables**

```bash
echo $bash            # /bin/bash
echo $bash_version    # e.g., 4.0.2.5
echo $pwd             # Current directory
echo $home            # Home directory
```

- **User-defined Variables**

```bash
Name='vinitha'
echo "My name is $Name"
# Output: My name is vinitha
```

### Append Text to Variable

```bash
Name='vinitha'
echo "My name is ${Name}R"

Word='string'
echo "This is ${Word}ing"
```

### Combine Variables

```bash
echo "${Name}${Word}."
```

---

## 📥 User Input

```bash
read Name
echo "Welcome, $Name"
```

---

## 🔢 Special Variables and Substitution

```bash
echo "Your user ID is ${UID}"
id -un       # Get username
```

---

## ✅ Conditionals

### `if` Statement

```bash
if [[ condition ]]; then
  command
fi
```

### `if-else` Example

```bash
num=10

if [[ $num -gt 5 ]]; then
  echo "Number is greater than 5"
else
  echo "Number is less than or equal to 5"
fi
```

---

## 🔤 String Comparison Operators

| Operator | Description      |
|----------|------------------|
| `==`     | Equal            |
| `!=`     | Not equal        |
| `-z`     | String is empty  |
| `-n`     | String is not empty |

---

## 📁 File Test Operators

| Operator | Tests if...        | Example            |
|----------|--------------------|--------------------|
| `-e`     | File exists        | `[ -e file.txt ]`  |
| `-f`     | Regular file       | `[ -f file.txt ]`  |
| `-d`     | Directory          | `[ -d dir ]`       |
| `-r`     | Readable           | `[ -r file.txt ]`  |
| `-w`     | Writable           | `[ -w file.txt ]`  |
| `-x`     | Executable         | `[ -x script.sh ]` |
| `-s`     | File not empty     | `[ -s file.txt ]`  |

---

## 🔢 Arithmetic Operators

```bash
((a + b))   # Addition
((a - b))   # Subtraction
((a * b))   # Multiplication
((a / b))   # Division
((a % b))   # Modulus
((a++))     # Increment
((--a))     # Decrement
```

---

## 🔁 Loops

### `for` Loop

```bash
for fruit in apple banana cherry
do
  echo "I like $fruit"
done
```

### `while` Loop

```bash
count=1
while [ $count -le 3 ]
do
  echo "Count is $count"
  ((count++))
done
```

---

## 📦 Arrays

```bash
Fruits=(apple banana watermelon)
echo "${Fruits[0]}"       # First element
echo "${Fruits[@]}"       # All elements
echo "${#Fruits[@]}"      # Length
```

---

## 🔐 Special Topics

- Random Data: `echo $RANDOM`
- Exit Status: `$?`
- Positional Parameters: `$0`, `$1`, `$2`, …, `$#`

---

## 🧪 User Management Script Goal

**Objective**: Automate user creation for a growing company to reduce manual work.

---

## 🛠️ System Commands (Common)

### System Info

- `uname -a` – Kernel name and version
- `hostname` – Show or set hostname
- `uptime` – System running time
- `top` – Live process monitor
- `free -h` – Memory status
- `lscpu` – CPU architecture
- `lsblk` – Block devices

### Disk & File Management

- `df -h` – Disk usage
- `du -sh` – Directory size

### User Management

```bash
useradd username
passwd username
userdel username
usermod -aG group username
id username
who
```

### Permissions

```bash
chmod 755 file
chown user:group file
ls -l
umask
```

### Package Management

```bash
apt update
apt upgrade
apt install package
apt remove package
```

### Services

```bash
systemctl status ssh
systemctl restart apache2
```

### Networking

```bash
ip a
ping google.com
ss -tuln
nmap localhost
curl http://example.com
```

### Logs

```bash
journalctl
dmesg
```

### Cron & Scheduling

```bash
crontab -e
at now + 1 minute
```

### Shutdown & Reboot

```bash
shutdown now
reboot
```
