# Linux Kernel and System Basics

## WEEK-1

---

## Kernel

The "father of the kernel," specifically referring to the Linux kernel, is **Linus Torvalds**.

The kernel is essentially the core of an operating system.  
It is the fundamental layer between computer hardware and software.  
It interacts with hardware and is often considered the nucleus of a computer’s operating system.  
It manages system resources such as the processor, memory, and device drivers.  
The kernel is stored in the computer’s memory.

### Types of Kernel

- **Monolithic Kernels**:  
  Entire OS including schedulers, file system, and device drivers is part of the kernel.  
  Can lead to complexity and potential instability if a service fails.

- **Microkernels**:  
  Run minimal services in kernel space for OS functionality.  
  Improves reliability and security.

- **Hybrid Kernels**:  
  Combine the advantages of monolithic and microkernels.  
  Some services run in kernel space, others in user space.

---

## Linux Distributions

A Linux distribution (or *distro*) is a complete operating system built around the Linux kernel.

### Components of a Linux Distribution

- Linux Kernel
- GNU Tools & Libraries
- Package Management System
- Software Applications
- Graphical User Interface (GUI)
- System Libraries & Utilities
- Bootloader

### Types of Distributions

- **General-Purpose**: Ubuntu, Fedora, Linux Mint  
- **Enterprise**: RHEL, CentOS, SUSE  
- **Security-Focused**: Kali Linux, Parrot OS  
- **Lightweight**: Lubuntu, Puppy Linux  
- **Specialized**: Ubuntu Studio, Edubuntu, OpenWrt

### ✅ Why Use a Linux Distribution?

- Open Source and Free
- Secure
- Customizable
- Ideal for Development
- Resource-Efficient
- Wide Variety
- Stable & Reliable
- Community Support

---

## Linux File System
root directory / - top of the file system
| Directory | Purpose                                        |
| --------- | ---------------------------------------------- |
| `/`       | Root of the file system                        |
| `/bin`    | Essential user binaries (e.g., `ls`, `cp`)     |
| `/sbin`   | System binaries (e.g., `init`, `reboot`)       |
| `/etc`    | System configuration files                     |
| `/home`   | User home directories                          |
| `/var`    | Variable data like logs (`/var/log`)           |
| `/usr`    | Secondary hierarchy: user apps and utilities   |
| `/tmp`    | Temporary files                                |
| `/dev`    | Device files (e.g., `/dev/sda`)                |
| `/proc`   | Virtual filesystem for process and kernel info |
| `/boot`   | Boot loader files (e.g., kernel images)        |
-\

| File               | Purpose                                                                                   |
| ------------------ | ----------------------------------------------------------------------------------------- |
| **`/etc/passwd`**  | Stores basic user account information like username, UID, GID, home directory, and shell. |
| **`/etc/shadow`**  | Stores encrypted user passwords and password expiration info (readable only by root).     |
| **`/etc/group`**   | Stores group information (group names, GIDs, and group members).                          |
| **`/etc/gshadow`** | Stores secure group information, including encrypted passwords for group access.          |


User management in Linux involves creating, modifying, and managing user accounts and groups to control access and permissions on the system.

| Task            | Command                 |
| --------------- | ----------------------- |
| Add user        | `sudo adduser username` |
| Delete user     | `sudo deluser username` |
| Change password | `passwd username`       |
| Modify user     | `usermod`               |
| List users      | `cat /etc/passwd`       |


### 🧩 Key Linux User Management Commands

#### Creating Users

sudo useradd -m -s /bin/bash username
sudo adduser username

#### Modifying Users

sudo usermod -aG groupname username

#### Deleting Users:
sudo userdel username

#### Managing Passwords

sudo passwd username
sudo passwd -l username   # Lock
sudo passwd -u username   # Unlock

#### Managing Groups

sudo groupadd groupname
sudo groupdel groupname
sudo gpasswd -a username groupname

Linux Permission Levels

4. Permission Levels

| Symbol | Meaning     | For Files                    | For Directories                    |
| ------ | ----------- | ---------------------------- | ---------------------------------- |
| `r`    | **Read**    | View file content            | List directory contents            |
| `w`    | **Write**   | Modify file content          | Add/delete files                   |
| `x`    | **Execute** | Run file as a program/script | Access directory (enter with `cd`) |

Viewiing permission:
ls -l

Breakdown:

-rwxr-xr--

- = regular file

rwx = user has read, write, and execute

r-x = group has read and execute

r-- = others have read only

chmod 755 file.txt   # rwxr-xr-x
chown user:group file.txt
username – login name

Modes of Use:
1. Symbolic Mode:

   chmod u+x script.sh    # Add execute for user
chmod g-w file.txt     # Remove write for group
chmod o=r file.txt     # Set read only for others

2. Numeric Mode
chmod 755 script.sh

Changing Ownership:
chown alice:staff file.txt

| Command | Purpose            |
| ------- | ------------------ |
| `ls -l` | View permissions   |
| `chmod` | Change permissions |
| `chown` | Change ownership   |
| `chgrp` | Change group only  |

x – password (stored in /etc/shadow)

UID – User ID

GID – Group ID

comment – optional (full name or description)

home_directory – default login directory

shell – default command shell

/etc/shadow-
encrypted passwords 
/etc/group
group information
john:x:1001:1001:John Doe:/home/john:/bin/bash


---

## File Permissions

### Symbolic Representation

`-rwxr-xr--`

- First character: File type (`-` for file, `d` for directory)
- Next 3: Owner (read, write, execute)
- Next 3: Group
- Next 3: Others

### Numeric Representation

- `r = 4`, `w = 2`, `x = 1`
- Example: `755` = Owner: rwx, Group: r-x, Others: r-x

### Changing Permissions

```bash
chmod u+x file
chmod 755 file
chown user:group file
umask 022
```

---

## Processes and Job Management
Learn about the Process Details, Creation, Termination, and States in Linux

Process Details:

A process is an instance of a running program.
Each process has:PID – Process ID
PPID – Parent Process ID
UID – User ID of the process owner
Command – The program being executed
ps aux
top
htop
Process Creation: A new process is created using the fork() system call, which duplicates the parent process.
The child process can then call exec() to replace itself with a new program.
echo "Process id = $$"
echo "Process id = $PPID"

 Example:
 sleep 60 &
 o/p" # 3249
 kill 3249
 | Term     | Meaning                          |
| -------- | -------------------------------- |
| `fork()` | Creates a child process          |
| `exec()` | Runs a new program in the child  |
| `PID`    | Process ID                       |
| `PPID`   | Parent Process ID                |
| `wait()` | Parent waits for child to finish |
| `exit()` | Process terminates               |

📌 Process Termination:
Process termination is the final stage of a process's lifecycle — when it stops running and its resources are released by the operating system.

| Signal    | Number | Description                                        |
| --------- | ------ | -------------------------------------------------- |
| `SIGTERM` | 15     | Graceful termination                               |
| `SIGKILL` | 9      | Forceful termination (cannot be caught or ignored) |
| `SIGINT`  | 2      | Interrupt (e.g., Ctrl+C)                           |
| `SIGQUIT` | 3      | Quit and dump core                                 |

### Process States

- **Running -R**
- **Sleeping-- S
- **Stopped - T
- **Zombie - Z
- Dead - x

- | Concept         | Explanation                               |
| --------------- | ----------------------------------------- |
| `exit()`        | Normal termination                        |
| `kill -9 <PID>` | Forcefully kills a process                |
| `SIGTERM`       | Allows cleanup before termination         |
| `SIGKILL`       | Immediately stops the process             |
| `wait()`        | Cleans up after child process termination |

Signals in Linux:

| Signal    | Code | Description                               |
| --------- | ---- | ----------------------------------------- |
| `SIGINT`  | `2`  | Interrupt from keyboard (`Ctrl+C`)        |
| `SIGTSTP` | `20` | Stop signal from keyboard (`Ctrl+Z`)      |
| `SIGKILL` | `9`  | Immediately terminate (cannot be ignored) |
| `SIGTERM` | `15` | Graceful termination request              |
| `SIGHUP`  | `1`  | Hangup signal (terminal closed)           |
| `SIGCONT` | `18` | Continue a stopped process                |

Sending Signals:

Using kill command:

kill -SIGTERM <PID>
kill -9 <PID>        # Force kill
kill -SIGCONT <PID>  # Resume a stopped process


| Key Combo | Signal Sent | Effect                                 |
| --------- | ----------- | -------------------------------------- |
| `Ctrl+C`  | `SIGINT`    | Interrupt/kill the process             |
| `Ctrl+Z`  | `SIGTSTP`   | Pause/stop the process                 |
| `fg`      | `SIGCONT`   | Resume a stopped process in foreground |

### Job Control:
Job control lets you manage multiple processes (jobs) in a single terminal session.

| State      | Description                              |
| ---------- | ---------------------------------------- |
| Running    | Actively executing                       |
| Stopped    | Suspended (e.g., with `Ctrl+Z`)          |
| Background | Running in background (`&`)              |
| Foreground | Running and tied to the current terminal |

| Command   | Description                       |
| --------- | --------------------------------- |
| `jobs`    | List current jobs                 |
| `bg`      | Resume a job in the background    |
| `fg`      | Resume a job in the foreground    |
| `kill %1` | Kill job number 1                 |
| `disown`  | Remove a job from shell job table |

Learn about the software distribution, package repositories and dependencies:

Linux distros use package managers to handle software and dependencies.

Repositories are sources of software packages.

### Software Distribution

- Packages include binaries, config, and metadata.

### Package Repositories

- Remote servers with software packages.

### Dependencies

- Required libraries that are automatically resolved during installation.


## File and Directory Management

```bash
ls       # List
pwd      # Print working directory
cd       # Change directory
mkdir    # Make directory
rmdir    # Remove directory
rm       # Remove file/directory
cp       # Copy
mv       # Move/Rename
```

---

## File Viewing and Editing

```bash
cat filename
less filename
nano filename
vim filename
```

---

## System Information

```bash
top
df
free
uname -a
```

---

## Networking

```bash
ping google.com
ifconfig
ip a
wget http://example.com
```

---

## Init System

- The **init system** is the first process (PID 1).
- It initializes system services, manages targets/runlevels, and handles shutdown.

Functions of the Init System:
1.Runs scripts and services
2.Starts, stops, restarts, and monitors services
3.Properly stops services during shutdown

| Init System  | Description                                                  | Used In                                            |
| ------------ | ------------------------------------------------------------ | -------------------------------------------------- |
| **SysVinit** | Traditional init system using numbered runlevels and scripts | Older distros (Debian, RHEL 6)                     |
| **Upstart**  | Event-driven replacement for SysV                            | Ubuntu (pre-15.04)                                 |
| **systemd**  | Modern init system and service manager                       | Most current distros (Ubuntu 16+, RHEL 7+, Fedora) |
| **OpenRC**   | Lightweight, used in Alpine Linux and Gentoo                 | Lightweight systems                                |

systemd is the most common init system today.

systemctl status
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl enable ssh

Resource monitoring means checking and analyzing how your system's hardware and processes are being used.
Process monitoring:A process is any running program
Which programs are running
How much CPU or memory they are using
Whether they are active, sleeping, or stuck

ps — snapshot of processes
top or htop — live, interactive view
pstree — shows parent-child process relationships

CPU Monitoring:
% of CPU used by user apps and the system
Idle time
Load on each core

top, htop
mpstat (from sysstat)
uptime (load average)

Memory Monitoring:
Total, used, and free memory
Swap usage (when RAM runs out)
Which processes are using the most memory
 Tools:

free -h

top, htop

vmstat
A thread is a lightweight part of a process. One process can have many threads doing different tasks at once

The /var/log directory is where Linux stores log files, which record events that happen on your system. These logs help you:

Troubleshoot errors

Monitor security and performance

Track system activity

black box of your Linux system.

/var/log contains system and application logs.

You can read logs with tail, less, or journalctl.

Logs help diagnose issues and monitor system health.

logrotate manages old logs to prevent overflow.
| File/Directory                                          | Description                                 |
| ------------------------------------------------------- | ------------------------------------------- |
| `/var/log/syslog` (Ubuntu) / `/var/log/messages` (RHEL) | General system activity logs                |
| `/var/log/kern.log`                                     | Kernel-related logs                         |
| `/var/log/auth.log`                                     | Authentication and sudo activity            |
| `/var/log/dmesg`                                        | Boot-time hardware messages                 |
| `/var/log/wtmp` & `/var/log/btmp`                       | Login and failed login records              |
| `/var/log/secure` (RHEL)                                | Security and authentication messages        |
| `/var/log/cron`                                         | Scheduled task logs                         |
| `/var/log/httpd/` or `/var/log/apache2/`                | Web server logs                             |
| `/var/log/apt/`                                         | Package install/update logs (Debian/Ubuntu) |


## Log Files in `/var/log`

- System Logs
- Authentication Logs
- Cron Logs
- Mail Logs
- Application Logs
- Background Services Logs

Cron jobs are automated tasks scheduled to run at specific times or intervals using a tool called cron. These are useful for repetitive tasks like:

Backing up files

Sending email alerts

Cleaning logs

Running scripts automatically


## Cron Jobs
Cron jobs are automated tasks scheduled to run at specific times or intervals using a tool called cron. These are useful for repetitive tasks like:

Backing up files

Sending email alerts

Cleaning logs

Running scripts automatically


```
* * * * * <command>
| | | | |7
0000000000000004


542222222222222222222203+66666666666666666666666665
| | | | +---- Day of week (0-6)
| | | +------ Month (1-12)
| | +-------- Day of month (1-31)
| +---------- Hour (0-23)
+------------ Minute (0-59)
```

### Examples

```bash
0 5 * * * /path/to/script.sh       # Daily at 5:00 AM
0 15 * * 1 /path/to/script.sh      # Mondays at 3:00 PM
*/5 * * * * /path/to/script.sh     # Every 5 minutes
```

### Commands

```bash
crontab -l   # View
crontab -e   # Edit
crontab -r   # Remove
```

---

## Common Linux Commands

| Command | Description                | Example                        |
|---------|----------------------------|--------------------------------|
| ls      | List directory contents    | `ls -l`                        |
| pwd     | Print working directory    | `pwd`                          |
| cd      | Change directory           | `cd /home/user`               |
| mkdir   | Create new directory       | `mkdir new_folder`           |
| rmdir   | Remove empty directory     | `rmdir old_folder`           |
| cp      | Copy files or directories  | `cp source.txt dest.txt`     |
| mv      | Move or rename files       | `mv old.txt new.txt`         |
| rm      | Remove files or directories| `rm file.txt`                |
| touch   | Create empty file          | `touch newfile.txt`          |
| ln      | Create links               | `ln -s target.txt link.txt`  |
