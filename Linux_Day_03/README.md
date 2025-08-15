# 🐧 Linux Day 03 – Command Reference & Examples

## 📌 Introduction
This document contains a **comprehensive list of essential Linux commands** covered on Day 03 of learning.  
It includes **explanations**, **usage syntax**, and **examples** for each command to help beginners and professionals quickly find the right command when working in Linux.  

---

## 📋 Command Summary Table

| Command   | Description | Example |
|-----------|-------------|---------|
| `uname`   | Displays system information | `uname -a` |
| `uptime`  | Shows how long the system has been running | `uptime -p` |
| `date`    | Displays or sets date/time | `date '+%Y-%m-%d %H:%M:%S'` |
| `who`     | Shows logged-in users | `who` |
| `whoami`  | Shows current username | `whoami` |
| `which`   | Shows full path of a command | `which python3` |
| `id`      | Displays UID & GID info | `id` |
| `sudo`    | Executes command as root | `sudo ls /root` |
| `shutdown`| Shuts down the system | `sudo shutdown now` |
| `reboot`  | Restarts the system | `sudo reboot` |
| `apt`     | Package management (Debian/Ubuntu) | `sudo apt update` |
| `apt-get` | Older apt package manager | `sudo apt-get install package` |
| `useradd` | Creates new user | `sudo useradd -m user1` |
| `passwd`  | Changes user password | `passwd user1` |
| `userdel` | Deletes a user | `sudo userdel -r user1` |
| `groupadd`| Creates a group | `sudo groupadd devs` |
| `gpasswd` | Manages group membership | `sudo gpasswd -a user devs` |
| `groupdel`| Deletes a group | `sudo groupdel devs` |
| `chmod`   | Changes permissions | `chmod 755 file.sh` |
| `umask`   | Sets default permissions mask | `umask 022` |
| `chown`   | Changes file owner/group | `sudo chown user:group file` |
| `chgrp`   | Changes file group | `sudo chgrp group file` |
| `zip`     | Compresses files | `zip archive.zip file1 file2` |
| `tar`     | Creates/extracts tar archives | `tar -cvf file.tar files/` |
| `scp`     | Securely copies files over SSH | `scp file.txt user@host:/path/` |
| `rsync`   | Efficient file sync | `rsync -avz folder/ user@host:/path/` |

---

## 📖 Detailed Command Explanations

### 1️⃣ `uname`
**Description:** Displays system and kernel information.  
**Usage:**
```bash
uname -a  # Show all system info
uname -r  # Show kernel release
```

---

### 2️⃣ `uptime`
**Description:** Shows how long the system has been running, load averages.  
**Usage:**
```bash
uptime
uptime -p  # Pretty format
```

---

### 3️⃣ `date`
**Description:** Displays or sets the system date and time.  
**Usage:**
```bash
date
date '+%Y-%m-%d %H:%M:%S'
```

---

### 4️⃣ `who` & `whoami`
**`who`** → Shows who is logged in.  
**`whoami`** → Shows current username.  
**Usage:**
```bash
who
whoami
```

---

### 5️⃣ `which`
**Description:** Shows full path of a command.  
**Usage:**
```bash
which ls
which python3
```

---

### 6️⃣ `id`
**Description:** Displays UID (user ID) and GID (group ID).  
**Usage:**
```bash
id
id username
```

---

### 7️⃣ `sudo`
**Description:** Executes commands as another user (root by default).  
**Usage:**
```bash
sudo ls /root
sudo shutdown now
```

---

### 8️⃣ `shutdown` & `reboot`
**Description:** Shuts down or restarts the system.  
**Usage:**
```bash
sudo shutdown now
sudo shutdown +10  # In 10 minutes
sudo reboot
```

---

### 9️⃣ `apt` & `apt-get`
**Description:** Package management for Debian/Ubuntu systems.  
**Usage:**
```bash
sudo apt update
sudo apt install package_name
sudo apt-get remove package_name
```

---

### 🔟 `useradd` & `passwd`
**Description:** Create a new user and set password.  
**Usage:**
```bash
sudo useradd -m user1
passwd user1
```

---

### 1️⃣1️⃣ `userdel`
**Description:** Deletes a user.  
**Usage:**
```bash
sudo userdel username
sudo userdel -r username  # Remove home directory
```

---

### 1️⃣2️⃣ `groupadd` & `gpasswd`
**Description:** Create groups and manage members.  
**Usage:**
```bash
sudo groupadd devs
sudo gpasswd -a user1 devs
sudo gpasswd -d user1 devs
```

---

### 1️⃣3️⃣ `chmod`
**Description:** Change file permissions.  
**Usage:**
```bash
chmod 755 script.sh
chmod u+x file.txt
```

---

### 1️⃣4️⃣ `umask`
**Description:** Set default permission mask for new files.  
**Usage:**
```bash
umask
umask 022
```

---

### 1️⃣5️⃣ `chown` & `chgrp`
**Description:** Change file ownership and group.  
**Usage:**
```bash
sudo chown user file
sudo chown user:group file
sudo chgrp group file
```

---

### 1️⃣6️⃣ `zip` & `tar`
**Description:** Compress and archive files.  
**Usage:**
```bash
zip archive.zip file1 file2
zip -r archive.zip folder/
tar -cvf archive.tar folder/
tar -xzvf archive.tar.gz
```

---

### 1️⃣7️⃣ `scp` & `rsync`
**Description:** Securely transfer or sync files between systems.  
**Usage:**
```bash
scp file.txt user@remote_host:/path/
rsync -avz folder/ user@remote_host:/path/
```

---

## 📚 Conclusion
This guide gives a **quick reference** and **detailed explanation** for essential Linux commands.  
You can use it as your **Day 03 Linux cheat sheet** for learning and practical use.
