# Day 3 – Linux Users, Groups, Files and File Management

## 1. System-Level Commands

System-level commands help us understand the operating system, system uptime, logged-in users, installed commands and system administration.

### 1. `uname` – Display System Information

Displays information about the operating system and kernel.

```bash
uname
uname -a
uname -r
```

- `uname` – Displays the kernel name.
- `uname -a` – Displays all available system information.
- `uname -r` – Displays the kernel release.

**Example:**

On Ubuntu, `uname` generally displays `Linux`.

On macOS, it displays `Darwin`.

### 2. `uptime` – Check System Uptime

Displays how long the machine has been running, the number of logged-in users and system load averages.

```bash
uptime
```

Example output:

```text
18:30:10 up 5 days,  3:20,  2 users,  load average: 0.10, 0.20, 0.15
```

- `18:30:10` – Current system time.
- `up 5 days, 3:20` – System has been running for 5 days and 3 hours 20 minutes.
- `2 users` – Number of logged-in user sessions.
- `load average` – Average system load over 1, 5 and 15 minutes.

### 3. `date` – Display Date and Time

Displays the current system date and time according to the configured timezone.

```bash
date
date -u
date "+%Y-%m-%d %H:%M:%S"
```

- `date` – Displays local system date and time.
- `date -u` – Displays date and time in UTC.
- Custom format – Displays date and time in the specified format.

### 4. `who` and `whoami` – Check Logged-In Users

**`who`** displays information about logged-in user sessions.

```bash
who
```

It can show:
- Username
- Terminal
- Login date and time
- Remote login information, when available

**`whoami`** displays the username of the current effective user.

```bash
whoami
```

### 5. `which` – Locate an Executable

Finds the executable file associated with a command by searching directories in the `$PATH` environment variable.

```bash
which python3
which docker
which terraform
which java
```

Example:

```text
/usr/bin/python3
```

**Important:** `which` displays the executable path, not the application's version.

To check a version, use:

```bash
python3 --version
docker --version
terraform --version
java -version
```

### 6. `id` – Display User and Group Information

Displays UID, GID and group membership for a user.

```bash
id
id mike
```

Example:

```text
uid=1001(mike) gid=1001(mike) groups=1001(mike),1002(devops)
```

- UID – User ID.
- GID – Primary Group ID.
- Groups – Groups to which the user belongs.

### 7. `sudo` – Execute Commands with Elevated Privileges

`sudo` allows an authorized user to execute a command with the privileges of another user, usually the root user.

```bash
sudo apt update
sudo systemctl restart nginx
```

**Important:** `sudo` is a command, not a group. On Ubuntu, eligible users are commonly given sudo permissions through the `sudo` group.

Check group membership:

```bash
groups
```

### 8. `shutdown` – Shut Down the System

Shuts down the Linux machine.

```bash
sudo shutdown now
```

Schedule shutdown after 5 minutes:

```bash
sudo shutdown +5
```

Cancel a scheduled shutdown:

```bash
sudo shutdown -c
```

**AWS EC2 note:** When an EC2 instance is stopped and started again, its automatically assigned public IPv4 address can change. An Elastic IP provides a static public IPv4 address.

### 9. `reboot` – Restart the System

Restarts the Linux machine.

```bash
sudo reboot
```

This command requires appropriate privileges.

### 10. `apt` – Advanced Package Tool

`apt` is the package manager commonly used in Ubuntu and Debian-based Linux distributions.

```bash
sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove nginx
sudo apt search nginx
sudo apt show nginx
```

- `update` – Refreshes package repository information.
- `upgrade` – Upgrades installed packages.
- `install` – Installs a package.
- `remove` – Removes a package.
- `search` – Searches for packages.
- `show` – Displays package information.

### 11. `yum` – Yellowdog Updater, Modified

A package manager used in older versions of CentOS and RHEL-based distributions.

```bash
sudo yum check-update
sudo yum install nginx
sudo yum remove nginx
sudo yum update
```

### 12. `dnf` – Dandified YUM

The modern successor to YUM, used by Fedora and newer RHEL-based distributions.

```bash
sudo dnf check-update
sudo dnf install nginx
sudo dnf remove nginx
sudo dnf update
```

### 13. `pacman` – Arch Linux Package Manager

Used in Arch Linux and its derivatives.

```bash
sudo pacman -Syu
sudo pacman -S nginx
sudo pacman -R nginx
```

### 14. `portage` – Gentoo Package Manager

Portage is the package management system used by Gentoo Linux. It supports source-based package installation and customization.

Example:

```bash
sudo emerge --sync
sudo emerge nginx
```

### 15. `rpm` – Red Hat Package Manager

RPM is a low-level package management system used by Red Hat-based distributions.

```bash
rpm -qa
rpm -qi nginx
rpm -qf /usr/bin/python3
```

- `-qa` – Lists installed RPM packages.
- `-qi` – Displays information about an installed package.
- `-qf` – Finds which package owns a file.

**YUM/DNF vs RPM:**

- RPM manages individual RPM packages.
- YUM and DNF provide higher-level package management, including repository access and dependency resolution.

---

## 2. User and Group Management Commands

Linux is a multi-user operating system. User and group management helps administrators control who can access files, directories and system resources.

### 1. `useradd` – Create a User

Creates a new Linux user.

```bash
sudo useradd mike
```

Create a user with a home directory:

```bash
sudo useradd -m mike
```

Check the user's information:

```bash
id mike
```

The `-m` option creates the user's home directory, usually `/home/mike`.

### 2. `whoami` – Check Current User

```bash
whoami
```

Displays the username of the current effective user.

### 3. `su` – Switch User

Switches to another user account.

```bash
su mike
```

For a login shell with the target user's environment:

```bash
su - mike
```

Check the current user:

```bash
whoami
```

### 4. `passwd` – Set or Change Password

Set a password for a user:

```bash
sudo passwd mike
```

Change your own password:

```bash
passwd
```

### 5. `userdel` – Delete a User

Deletes a user account.

```bash
sudo userdel mike
```

To delete the user and their home directory:

```bash
sudo userdel -r mike
```

**Caution:** The `-r` option removes the user's home directory and mail spool. Check the data before using it.

### 6. `groupadd` – Create a Group

Creates a new group.

```bash
sudo groupadd devops
```

View group information:

```bash
cat /etc/group
```

Check a specific user's groups:

```bash
groups mike
```

### 7. `gpasswd` – Manage Group Membership

Add a single user to a group:

```bash
sudo gpasswd -a mike devops
```

Alternatively, use `usermod`:

```bash
sudo usermod -aG devops mike
```

**Important:** The `-aG` options append the user to supplementary groups without removing existing group memberships.

To set the complete member list of a group:

```bash
sudo gpasswd -M carl,monty,michael tester
```

**Caution:** `-M` replaces the group's existing supplementary member list. Use it carefully.

Check group membership:

```bash
cat /etc/group
groups mike
id mike
```

### 8. `groupdel` – Delete a Group

Deletes a group.

```bash
sudo groupdel tester
```

A group generally cannot be deleted while it is the primary group of an existing user.

### Useful User and Group Files

| File | Purpose |
|---|---|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Secure password hashes and password aging information |
| `/etc/group` | Group information |
| `/etc/gshadow` | Secure group information |

Example:

```bash
cat /etc/passwd
cat /etc/group
```

---

## 3. File Permission Commands

Linux file permissions control who can read, write or execute files and directories.

### 1. `umask` – Set Default Permissions Mask

`umask` controls which permissions are removed when new files and directories are created.

```bash
umask
```

Set a temporary umask:

```bash
umask 022
```

Example:

For a typical Linux default:
- New files start with base permissions `666`.
- New directories start with base permissions `777`.

With `umask 022`:

| Type | Calculation | Result |
|---|---|---|
| File | 666 with 022 masked | 644 |
| Directory | 777 with 022 masked | 755 |

This means:
- Files: Owner can read/write; group and others can read.
- Directories: Owner can read/write/enter; group and others can read/enter.

**Note:** Umask removes permissions; it does not grant permissions. The actual result also depends on the application creating the file.

### 2. `ls -l` – List Files with Permissions

Displays detailed information about files and directories.

```bash
ls -l
```

Example:

```text
-rw-rw-r-- 1 mike devops 3614 Jul 17 12:02 demo_file.txt
```

Explanation:

| Part | Meaning |
|---|---|
| `-` | Regular file |
| `rw-` | Owner permissions |
| `rw-` | Group permissions |
| `r--` | Others' permissions |
| `mike` | Owner |
| `devops` | Group |
| `3614` | File size in bytes |
| `demo_file.txt` | Filename |

The first character can indicate:
- `-` – Regular file
- `d` – Directory
- `l` – Symbolic link

### 3. `chmod` – Change File Permissions

Changes permissions for files and directories.

There are two common ways to use `chmod`.

**A. Numeric method**

| Number | Permission |
|---|---|
| 4 | Read (`r`) |
| 2 | Write (`w`) |
| 1 | Execute (`x`) |

Examples:

```bash
chmod 755 script.sh
chmod 644 demo_file.txt
chmod 700 private_folder
```

Permission breakdown:

| Number | Owner | Group | Others |
|---|---|---|---|
| 755 | 7 = rwx | 5 = r-x | 5 = r-x |
| 644 | 6 = rw- | 4 = r-- | 4 = r-- |
| 700 | 7 = rwx | 0 = --- | 0 = --- |

**B. Symbolic method**

```bash
chmod u+x script.sh
chmod g+w demo_file.txt
chmod o-r demo_file.txt
chmod a+r demo_file.txt
```

- `u` – User/owner
- `g` – Group
- `o` – Others
- `a` – All
- `+` – Add permission
- `-` – Remove permission
- `=` – Set exact permission

**Directory permission note:**
- Read (`r`) allows listing directory entries.
- Write (`w`) allows creating, deleting or renaming entries, subject to other permission checks.
- Execute (`x`) allows entering/traversing the directory.

### 4. `chown` – Change File Owner

Changes the owner of a file or directory.

```bash
sudo chown mike demo_file.txt
```

Change both owner and group:

```bash
sudo chown mike:devops demo_file.txt
```

Change ownership recursively:

```bash
sudo chown -R mike:devops project/
```

### 5. `chgrp` – Change Group Ownership

Changes the group associated with a file or directory.

```bash
sudo chgrp devops demo_file.txt
```

Change group recursively:

```bash
sudo chgrp -R devops project/
```

Verify ownership and permissions:

```bash
ls -l
```

Example:

```text
-rw-rw-r-- 1 mike devops 3614 Jul 17 12:02 demo_file.txt
```

Here:
- `mike` is the file owner.
- `devops` is the file's group.

---

## 4. File Compression and Archiving Commands

Compression reduces file size, while archiving combines multiple files and directories into one archive.

### 1. `zip` – Create a ZIP Archive

Compresses files and directories into a `.zip` archive.

```bash
zip -r kgf.zip linux_for_devops/
```

- `-r` – Recursively includes files and subdirectories.

Example:

```text
adding: linux_for_devops/
adding: linux_for_devops/dummy_file.txt
adding: linux_for_devops/demo_file.txt
```

### 2. `unzip` – Extract a ZIP Archive

Extract a ZIP archive:

```bash
unzip kgf.zip
```

Extract into a specific directory:

```bash
unzip kgf.zip -d extracted_files/
```

List archive contents without extracting:

```bash
unzip -l kgf.zip
```

### Example: ZIP and UNZIP

Create a directory and copy the archive:

```bash
mkdir coco
cp kgf.zip coco/
cd coco
```

Extract the archive:

```bash
unzip kgf.zip
```

Check the extracted files:

```bash
ls
```

### 3. `gzip` – Compress a File

Compresses an individual file using gzip.

```bash
gzip demo_file.txt
```

This normally creates:

```text
demo_file.txt.gz
```

To keep the original file:

```bash
gzip -k demo_file.txt
```

### 4. `gunzip` – Decompress a GZIP File

Extracts a `.gz` file.

```bash
gunzip demo_file.txt.gz
```

### 5. `tar` – Archive Files and Directories

`tar` combines files and directories into a single archive. It can also use compression tools such as gzip.

Create a compressed archive:

```bash
tar -cvzf cloud.tar.gz cloud/
```

Extract a compressed archive:

```bash
tar -xvzf cloud.tar.gz
```

Extract into a specific directory:

```bash
mkdir extracted
tar -xvzf cloud.tar.gz -C extracted/
```

List archive contents:

```bash
tar -tvf cloud.tar.gz
```

**Common TAR options:**

| Option | Meaning |
|---|---|
| `-c` | Create an archive |
| `-x` | Extract an archive |
| `-v` | Verbose output |
| `-z` | Use gzip compression |
| `-f` | Specify archive filename |
| `-t` | List archive contents |
| `-C` | Specify destination directory |

**Remember:**
- `zip` creates ZIP archives.
- `gzip` compresses individual files.
- `gunzip` decompresses gzip files.
- `tar` bundles files and directories; with `-z`, it also uses gzip compression.

---

## 5. File Transfer Commands

File transfer commands help us move files between local machines and remote Linux servers.

### 1. `scp` – Secure Copy

`scp` securely copies files between systems using SSH.

**Example 1: Copy a Local File to a Remote Linux Server**

```bash
scp -i ~/Downloads/nv.cer test.sh ubuntu@3.109.124.17:/home/ubuntu/
```

Explanation:
- `scp` – Secure copy command.
- `-i` – Specifies the SSH private key.
- `test.sh` – Local file to transfer.
- `ubuntu` – Remote username.
- `3.109.124.17` – Remote server IP address.
- `/home/ubuntu/` – Destination directory.

**Example 2: Copy a Remote Directory to a Local Machine**

```bash
scp -i ~/Downloads/nv.cer -r ubuntu@3.109.124.17:/home/ubuntu/linux_for_devops .
```

- `-r` – Copies directories recursively.
- `.` – Current local directory.

**Important:** Protect your private SSH key. On Linux/macOS, SSH may require restrictive permissions:

```bash
chmod 400 ~/Downloads/nv.cer
```

### 2. `rsync` – Remote Synchronization

`rsync` is a utility for synchronizing files and directories locally or between remote machines.

It is useful for:
- Backups
- File synchronization
- Website deployments
- Server-to-server transfers
- Transferring only changed file data where possible

**Example 1: Synchronize a Local Directory**

```bash
rsync -av source/ destination/
```

**Example 2: Copy a Local Directory to a Remote Server**

```bash
rsync -av -e "ssh -i ~/Downloads/nv.cer" ./project/ ubuntu@3.109.124.17:/home/ubuntu/project/
```

**Example 3: Copy a Remote Directory to a Local Machine**

```bash
rsync -av -e "ssh -i ~/Downloads/nv.cer" ubuntu@3.109.124.17:/home/ubuntu/project/ ./project/
```

**Example 4: Delete Destination Files That Are No Longer in the Source**

```bash
rsync -av --delete source/ destination/
```

**Caution:** `--delete` removes destination files that do not exist in the source. Always verify source and destination before running it.

**Common options:**

| Option | Meaning |
|---|---|
| `-a` | Archive mode; preserves common file attributes and copies recursively |
| `-v` | Verbose output |
| `-z` | Compress data during transfer |
| `-h` | Human-readable numbers |
| `--delete` | Delete destination files absent from source |
| `--progress` | Show transfer progress |

**SCP vs RSYNC:**

| SCP | RSYNC |
|---|---|
| Secure file copying | File synchronization and transfer |
| Commonly copies the selected files/directories | Can identify and transfer changed data |
| Useful for straightforward copies | Useful for recurring backups and synchronization |
| Uses SSH for remote transfers | Can use SSH for remote transfers |

---

## 6. Hands-On Practice – Day 3

Practice these commands on an Ubuntu virtual machine or EC2 instance. Use a test machine, not a production server.

### Exercise 1: System Information

```bash
uname -a
uptime
date
date -u
who
whoami
id
which python3
python3 --version
```

### Exercise 2: Create Users and Groups

```bash
sudo groupadd devops
sudo useradd -m mike
sudo passwd mike
sudo usermod -aG devops mike
id mike
groups mike
```

### Exercise 3: Create and Change File Permissions

```bash
touch demo_file.txt
ls -l demo_file.txt
sudo chown mike:devops demo_file.txt
chmod 640 demo_file.txt
ls -l demo_file.txt
```

### Exercise 4: Compression and Extraction

```bash
mkdir linux_for_devops
touch linux_for_devops/file1.txt
touch linux_for_devops/file2.txt

zip -r linux_for_devops.zip linux_for_devops/
unzip -l linux_for_devops.zip

tar -cvzf linux_for_devops.tar.gz linux_for_devops/
tar -tvf linux_for_devops.tar.gz
```

### Exercise 5: File Transfer

Try transferring a test file to your remote Ubuntu server:

```bash
scp -i ~/Downloads/nv.cer test.sh ubuntu@YOUR_SERVER_IP:/home/ubuntu/
```

Then experiment with:

```bash
rsync -av ./project/ ubuntu@YOUR_SERVER_IP:/home/ubuntu/project/
```

Replace `YOUR_SERVER_IP` with your actual server address.

---

## 7. Important DevOps Interview Questions

1. What is the difference between `uname` and `uptime`?
2. What is the difference between `who` and `whoami`?
3. What is the difference between `which` and `whereis`?
4. What is UID and GID in Linux?
5. What is the purpose of `sudo`?
6. What is the difference between `useradd` and `usermod`?
7. What is the difference between a primary group and a supplementary group?
8. What is the difference between `chmod`, `chown` and `chgrp`?
9. What is umask, and how does it affect new files?
10. Explain Linux permissions `755`, `644` and `700`.
11. What is the difference between `zip` and `gzip`?
12. What is the difference between `tar` and `gzip`?
13. What is the difference between `scp` and `rsync`?
14. What is the difference between `apt`, `yum` and `dnf`?
15. What is the difference between RPM and YUM/DNF?

---

## 8. Real-World DevOps Use Cases

| Command | DevOps Use Case |
|---|---|
| `uname` | Identify OS and kernel information |
| `uptime` | Check server uptime and load |
| `id` | Verify service-account permissions |
| `sudo` | Perform administrative tasks |
| `useradd` | Create application or deployment users |
| `groupadd` | Create teams or access-control groups |
| `chmod` | Set script and file permissions |
| `chown` | Assign application directory ownership |
| `umask` | Control default permissions |
| `tar` | Package application files and backups |
| `gzip` | Compress logs and files |
| `scp` | Copy files to remote servers |
| `rsync` | Synchronize deployment files and backups |
| `apt` / `dnf` | Install system packages and dependencies |

**Day 3 Learning Outcome:** Understand Linux system information, user and group administration, file permissions, compression, archiving and secure file transfers.
