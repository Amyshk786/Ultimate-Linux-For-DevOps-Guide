# Day 2 – Linux Basic Commands for DevOps Engineers

Linux commands are essential for DevOps engineers because they help manage files, directories, processes, storage, memory, networking and remote servers.

This guide covers commonly used Linux commands with practical examples.

---

## 1. File and Directory Management Commands

### 1. `ls` – List Directory Contents

Lists files and directories in the current location.

```bash
ls
```

Useful options:

```bash
ls -l       # Long listing format
ls -a       # Show hidden files
ls -lh      # Human-readable file sizes
ls -ltr     # Sort by modification time, oldest first
ls -R       # List directories recursively
```

### 2. `cd` – Change Directory

Used to move from one directory to another.

```bash
cd /home/ubuntu
cd Documents
cd ..        # Move one directory up
cd ~         # Go to the home directory
cd -         # Return to the previous directory
```

### 3. `pwd` – Print Working Directory

Displays the absolute path of the current working directory.

```bash
pwd
```

Example:

```text
/home/ubuntu
```

### 4. `mkdir` – Create a Directory

Creates a new directory.

```bash
mkdir devops
```

Create multiple directories:

```bash
mkdir devops linux docker
```

Create nested directories:

```bash
mkdir -p devops/linux/commands
```

The `-p` option creates parent directories if they do not exist.

### 5. `rm` and `rmdir` – Delete Files and Directories

**Remove a file:**

```bash
rm file.txt
```

**Remove an empty directory:**

```bash
rmdir devops
```

**Remove a directory and its contents recursively:**

```bash
rm -r devops
```

**Forcefully remove files and directories:**

```bash
rm -rf devops
```

- `-r` – Recursive deletion.
- `-f` – Force deletion without prompting for confirmation.

**Caution:** `rm -rf` can permanently delete important data. Always verify the path before executing it, especially on production servers.

### 6. `cat` and `zcat` – Display File Contents

**`cat`** displays file contents.

```bash
cat file.txt
```

Create a file and add content:

```bash
cat > file.txt
```

Press `Ctrl + D` to finish entering content.

Display multiple files:

```bash
cat file1.txt file2.txt
```

**`zcat`** displays the contents of gzip-compressed files without manually extracting them.

```bash
zcat file.txt.gz
```

### 7. `touch` – Create an Empty File

Creates an empty file if it does not exist. If the file already exists, it updates its timestamps.

```bash
touch file.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

### 8. `head` – Display the First Lines of a File

Displays the first 10 lines by default.

```bash
head file.txt
```

Display the first 5 lines:

```bash
head -n 5 file.txt
```

### 9. `tail` – Display the Last Lines of a File

Displays the last 10 lines by default.

```bash
tail file.txt
```

Display the last 5 lines:

```bash
tail -n 5 file.txt
```

**`tail -f` – Monitor Logs in Real Time**

```bash
tail -f /var/log/syslog
```

It continuously displays new lines added to the log file.

Another useful option:

```bash
tail -F application.log
```

`-F` retries opening the file if it is recreated or rotated. This is useful for monitoring application logs.

**DevOps use case:** Monitoring application logs, deployment logs and troubleshooting production issues.

### 10. `less` and `more` – View File Contents

Both commands allow you to view files page by page.

```bash
less file.txt
more file.txt
```

`less` is generally more flexible because it supports backward and forward navigation and searching.

Useful `less` keyboard shortcuts:

| Key | Action |
|---|---|
| `Space` | Next page |
| `b` | Previous page |
| `/word` | Search forward |
| `n` | Next search result |
| `q` | Quit |

### 11. `cp` – Copy Files and Directories

Copy a file:

```bash
cp file.txt backup.txt
```

Copy a file into another directory:

```bash
cp file.txt /home/ubuntu/backup/
```

Copy a directory recursively:

```bash
cp -r devops backup/
```

### 12. `mv` – Move or Rename Files and Directories

Rename a file:

```bash
mv oldname.txt newname.txt
```

Move a file into another directory:

```bash
mv file.txt /home/ubuntu/backup/
```

Move a directory:

```bash
mv devops /home/ubuntu/
```

### 13. `wc` – Word Count

Displays the number of lines, words and bytes in a file.

```bash
wc file.txt
```

Example output:

```text
5  20  120 file.txt
```

This means:
- 5 lines
- 20 words
- 120 bytes

Useful options:

```bash
wc -l file.txt    # Count lines
wc -w file.txt    # Count words
wc -c file.txt    # Count bytes
wc -m file.txt    # Count characters
```

Count lines in multiple files:

```bash
wc -l file1.txt file2.txt
```

### 14. `vi` – Text Editor

`vi` is a command-line text editor available on many Unix and Linux systems.

Open or create a file:

```bash
vi file.txt
```

Important `vi` commands:

| Command | Purpose |
|---|---|
| `i` | Enter insert mode |
| `Esc` | Return to command mode |
| `:w` | Save the file |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `dd` | Delete the current line |
| `yy` | Copy the current line |
| `p` | Paste copied content |
| `/word` | Search for a word |
| `u` | Undo the last change |

**Important:** `vi` has different modes. Press `Esc` before entering commands such as `:wq`.

---

## 2. Linux Links – Hard Link and Soft Link

Linux supports two common types of file links.

### 15. `ln` – Create Hard Links and Symbolic Links

#### A. Soft Link (Symbolic Link)

A soft link is a pointer to another file or directory.

Create a soft link:

```bash
ln -s /home/ubuntu/devops/cloud/newfile.txt soft-link
```

Check the link:

```bash
ls -l
```

Example:

```text
soft-link -> /home/ubuntu/devops/cloud/newfile.txt
```

If the original file is deleted or moved, the symbolic link may become a broken link because its target is no longer available.

A broken symbolic link may appear in a different color depending on your terminal configuration.

#### B. Hard Link

A hard link is another directory entry that refers to the same underlying file data (inode).

Create a hard link:

```bash
ln /home/ubuntu/devops/cloud/newfile.txt hard-link
```

Check inode numbers:

```bash
ls -li
```

If the original filename is deleted, the hard link can still access the file data.

**Difference between Hard Link and Soft Link:**

| Hard Link | Soft Link |
|---|---|
| Refers to the same inode | Stores a path to the target |
| Usually cannot link directories | Can link files and directories |
| Normally cannot cross filesystem boundaries | Can cross filesystem boundaries |
| Remains usable if another hard-linked filename is deleted | Can become broken if the target is removed |
| Created using `ln` | Created using `ln -s` |

**Remember:** Deleting the original filename does not delete the underlying data while another hard link still refers to it. The data is removed when its link count reaches zero and no other references keep it in use.

---

## 3. Text Processing Commands

### 16. `cut` – Extract Specific Parts of a Line

Used to extract selected bytes, characters or fields from text.

Extract bytes 1 to 4:

```bash
cut -b 1-4 demo_file.txt
```

Extract the first column from a comma-separated file:

```bash
cut -d ',' -f 1 employees.csv
```

- `-b` – Select bytes.
- `-c` – Select characters.
- `-d` – Specify the delimiter.
- `-f` – Select fields.

### 17. `tee` – Display and Save Output

`tee` reads input and writes it both to the terminal and to a file.

```bash
echo "Hello" | tee file.txt
```

This displays `Hello` on the screen and writes it to `file.txt`.

Append instead of overwriting:

```bash
echo "Welcome to Linux" | tee -a file.txt
```

Useful when saving command output:

```bash
df -h | tee disk-usage.txt
```

### 18. `sort` – Sort File Contents

Sorts lines alphabetically by default.

```bash
sort names.txt
```

Numerical sorting:

```bash
sort -n numbers.txt
```

Reverse sorting:

```bash
sort -r names.txt
```

Save sorted output:

```bash
sort names.txt -o sorted_names.txt
```

### 19. `clear` – Clear the Terminal Screen

Clears the visible terminal screen.

```bash
clear
```

Keyboard shortcut in many terminals:

```text
Ctrl + L
```

### 20. `diff` – Compare Two Files

Displays differences between two files.

```bash
diff file1.txt file2.txt
```

Useful option:

```bash
diff -u file1.txt file2.txt
```

`-u` displays differences in unified format, which is commonly used in code reviews and patch files.

---

## 4. Remote Access and Disk Management

### 21. `ssh` – Secure Shell

SSH allows us to connect securely to a remote Linux machine.

```bash
ssh ubuntu@192.168.1.10
```

Connect using a private key:

```bash
ssh -i ~/Downloads/nv.cer ubuntu@3.109.124.17
```

Connect using a custom port:

```bash
ssh -p 2222 ubuntu@192.168.1.10
```

By default, SSH uses TCP port `22`.

**DevOps use case:** Connecting to AWS EC2 instances, Linux servers and remote infrastructure.

### 22. `df` – Disk Filesystem Usage

Displays available and used disk space on mounted filesystems.

```bash
df
```

Human-readable format:

```bash
df -h
```

Display information for a particular filesystem path:

```bash
df -h /home/ubuntu
```

### 23. `du` – Disk Usage

Displays the disk space used by files and directories.

```bash
du file.txt
```

Human-readable format:

```bash
du -h
```

Display total size of a directory:

```bash
du -sh /home/ubuntu
```

Display sizes of directories inside the current directory:

```bash
du -h --max-depth=1 .
```

**Difference between `df` and `du`:**

| `df` | `du` |
|---|---|
| Shows filesystem-level disk usage | Shows file and directory usage |
| Displays available and used space | Helps identify which directories consume space |
| Useful for checking disk capacity | Useful for finding large directories |

---

## 5. Process Management Commands

### 24. `ps` – Display Running Processes

Displays information about processes running on the system.

```bash
ps
```

Display all processes:

```bash
ps -ef
```

Display processes in a detailed format:

```bash
ps aux
```

Find a specific process:

```bash
ps -ef | grep nginx
```

Common process information:
- PID – Process ID.
- PPID – Parent Process ID.
- USER – Process owner.
- CPU and memory usage.
- Command being executed.

### 25. `top` – Monitor System Processes

Displays a real-time view of processes and system resource usage.

```bash
top
```

It provides information about:
- CPU usage
- Memory usage
- Running processes
- Process IDs
- Load averages
- Process states

Common process states include:

| State | Meaning |
|---|---|
| `R` | Running or runnable |
| `S` | Interruptible sleep |
| `D` | Uninterruptible sleep |
| `T` | Stopped or traced |
| `Z` | Zombie |

**Important:** A killed process is not a separate process state displayed by `top`. A zombie is a process that has exited but whose parent has not yet collected its exit status.

Press `q` to exit `top`.

### 26. `fuser` – Identify Processes Using a File or Port

Identifies processes using a particular file, directory or filesystem.

```bash
fuser file.txt
```

Check which process is using TCP port 8080:

```bash
sudo fuser -v -n tcp 8080
```

Check which process is using port 80:

```bash
sudo fuser -v -n tcp 80
```

**DevOps use case:** Troubleshooting port conflicts when an application cannot start because another process is already using the port.

### 27. `kill` – Send a Signal to a Process

Sends a signal to a process using its PID.

```bash
kill 1234
```

By default, `kill` sends the `SIGTERM` signal, requesting the process to terminate gracefully.

Forcefully terminate a process:

```bash
kill -9 1234
```

Send a specific signal:

```bash
kill -SIGTERM 1234
```

**Important:** Prefer `SIGTERM` before using `SIGKILL` (`-9`). Forceful termination does not allow the process to clean up resources.

Find the PID first:

```bash
ps -ef | grep nginx
```

### 28. `nohup` – Run a Command Immune to Hangup Signals

`nohup` allows a command to continue running after the terminal session ends, provided the process is not otherwise terminated.

Example:

```bash
nohup python3 app.py &
```

By default, output is redirected to a file named `nohup.out` if it cannot be written to the terminal.

Specify your own log file:

```bash
nohup python3 app.py > app.log 2>&1 &
```

Explanation:
- `nohup` – Ignore hangup signals.
- `>` – Redirect standard output to a file.
- `2>&1` – Redirect standard error to the same destination.
- `&` – Run the command in the background.

Monitor the output:

```bash
tail -f app.log
```

**Important:** `nohup` is not a full process supervisor. For production applications, consider `systemd`, Kubernetes or another process manager.

---

## 6. Memory and System Performance Commands

### 29. `free` – Display Memory Usage

Displays RAM and swap usage.

```bash
free
```

Human-readable output:

```bash
free -h
```

Example:

```text
               total        used        free
Mem:           7.7Gi       2.1Gi       1.2Gi
Swap:          2.0Gi          0B       2.0Gi
```

Useful options:

```bash
free -m
free -g
free -h
```

- `-m` – Display values in MB.
- `-g` – Display values in GB.
- `-h` – Human-readable output.

### 30. `vmstat` – Virtual Memory Statistics

Displays information about system processes, memory, swap, I/O, CPU activity and system activity.

```bash
vmstat
```

Display information every 2 seconds:

```bash
vmstat 2
```

Display 5 reports at 2-second intervals:

```bash
vmstat 2 5
```

Display active and inactive memory:

```bash
vmstat -a
```

Example output:

```text
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free  inact active   si   so   bi   bo   in   cs us sy id wa st
 0  0      0 103632 521928 128340    0    0    6    5   19   31  0  0 100  0  0
```

**Important columns:**

| Column | Meaning |
|---|---|
| `r` | Runnable processes |
| `b` | Processes blocked waiting for resources |
| `swpd` | Virtual memory used |
| `free` | Free memory |
| `inact` | Inactive memory |
| `active` | Active memory |
| `si` | Memory swapped in per second |
| `so` | Memory swapped out per second |
| `bi` | Blocks received from block devices |
| `bo` | Blocks sent to block devices |
| `in` | Interrupts per second |
| `cs` | Context switches per second |
| `us` | CPU time spent in user processes |
| `sy` | CPU time spent in system/kernel |
| `id` | CPU idle time |
| `wa` | CPU time waiting for I/O |
| `st` | CPU time stolen by the hypervisor |

**DevOps use case:** Investigating high CPU usage, memory pressure, swapping and disk I/O bottlenecks.

---

## 7. Quick Command Reference

| Category | Commands | Purpose |
|---|---|---|
| Navigation | `ls`, `cd`, `pwd` | Navigate directories |
| Directory management | `mkdir`, `rmdir` | Create and remove directories |
| File management | `touch`, `cp`, `mv`, `rm` | Create, copy, move and delete files |
| File viewing | `cat`, `zcat`, `head`, `tail`, `less`, `more` | Read file contents |
| File information | `wc`, `stat` | Inspect file information |
| Links | `ln`, `ln -s` | Create hard and symbolic links |
| Text processing | `cut`, `sort`, `diff`, `tee` | Process and compare text |
| Remote access | `ssh` | Connect to remote servers |
| Disk management | `df`, `du` | Check disk usage |
| Process management | `ps`, `top`, `kill`, `fuser` | Inspect and manage processes |
| Background execution | `nohup` | Run commands after terminal disconnect |
| Memory monitoring | `free`, `vmstat` | Monitor memory and system performance |

---

## 8. Hands-On Practice – Day 2

Run these commands on an Ubuntu VM or EC2 test instance.

### Exercise 1: File and Directory Operations

```bash
mkdir devops-practice
cd devops-practice
pwd

touch file1.txt file2.txt
ls -l

mkdir backup
cp file1.txt backup/
mv file2.txt renamed_file.txt

ls -R
```

### Exercise 2: File Viewing and Text Processing

```bash
echo "Welcome to Linux DevOps" > file1.txt
cat file1.txt

head -n 5 file1.txt
tail -n 5 file1.txt
wc file1.txt

cut -c 1-4 file1.txt
sort file1.txt
```

### Exercise 3: Hard Link and Soft Link

```bash
touch original.txt

ln original.txt hard-link.txt
ln -s original.txt soft-link.txt

ls -li
```

Compare inode numbers and then experiment with deleting the original filename.

### Exercise 4: Disk and Memory Monitoring

```bash
df -h
du -sh .
free -h
vmstat 2 5
```

### Exercise 5: Process Management

```bash
sleep 300 &
ps -ef | grep sleep
top
```

Find the process ID and terminate the test process:

```bash
kill PID
```

Replace `PID` with the actual process ID.

### Exercise 6: Background Execution and Logs

```bash
nohup bash -c 'while true; do date; sleep 5; done' > app.log 2>&1 &
```

Monitor logs:

```bash
tail -f app.log
```

Stop the test process when finished.

---

## 9. DevOps Interview Questions

1. What is the difference between `ls`, `ls -l` and `ls -a`?
2. What is the difference between `rm -r` and `rmdir`?
3. What is the difference between `cat`, `less` and `more`?
4. What is the difference between `head` and `tail`?
5. Why do DevOps engineers use `tail -f`?
6. What is the difference between `cp` and `mv`?
7. What is the difference between hard links and soft links?
8. What is an inode in Linux?
9. What is the difference between `cut` and `awk`?
10. What is the purpose of `tee`?
11. What is the difference between `df` and `du`?
12. What is the difference between `ps` and `top`?
13. What is a zombie process?
14. What is the difference between `kill` and `kill -9`?
15. What is the purpose of `nohup`?
16. What is the difference between `free` and `vmstat`?
17. How do you identify which process is using port 8080?
18. How do you connect to an AWS EC2 instance using SSH?
19. How do you monitor application logs in real time?
20. How do you identify whether a Linux server is running out of disk space?

---

## 10. Real-World DevOps Scenarios

| Scenario | Commands to Use |
|---|---|
| Application logs are growing | `tail`, `less`, `du` |
| Server disk is almost full | `df -h`, `du -sh` |
| Application cannot start because a port is busy | `fuser`, `ps`, `kill` |
| Need to connect to an EC2 server | `ssh` |
| Need to inspect memory pressure | `free -h`, `vmstat` |
| Need to compare configuration files | `diff` |
| Need to create a backup directory | `mkdir`, `cp`, `tar` |
| Need to monitor a running application | `ps`, `top`, `tail -f` |
| Need to run a script after disconnecting SSH | `nohup` |
| Need to find a large log file | `du`, `find`, `ls -lh` |

**Day 2 Learning Outcome:** Understand Linux navigation, file operations, links, text processing, remote access, disk management, process management and system performance monitoring.
