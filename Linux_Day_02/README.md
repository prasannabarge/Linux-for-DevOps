# 🐧 Linux Day 02 - Command Reference

This repository contains the **Linux commands learned on Day 02** of practice.  
Each command includes its **purpose**, **usage**, and **examples** for better understanding.  
Ideal for beginners learning Linux or anyone needing a quick reference.

---

## 📌 Commands Overview

Below is a table with **command names**, their **explanation**, and **examples** (both yours & additional).

| Command | Explanation | Example (Yours) | Example (Additional) |
|---------|-------------|-----------------|----------------------|
| `date` | Displays the current date and time. | `date` | `date +"%Y-%m-%d %H:%M:%S"` |
| `ls` | Lists files and directories. | `ls` | `ls -l` |
| `cd` | Changes the directory. | `cd ycis` | `cd /var/log` |
| `pwd` | Prints the current working directory. | `pwd` | `pwd` |
| `mkdir` | Creates a new directory. | `mkdir bca` | `mkdir projects` |
| `touch` | Creates a new empty file. | `touch demo.txt` | `touch notes.md` |
| `rm` | Removes a file. | `rm demo.txt` | `rm temp.log` |
| `rm -r` | Removes a directory and its contents recursively. | `rm -r bca` | `rm -r old_project` |
| `rmdir` | Removes an empty directory. | `rmdir bca` | `rmdir empty_dir` |
| `cat` | Displays file content. | `cat demo.txt` | `cat /etc/passwd` |
| `echo` | Displays a message or assigns text to a file. | `echo "Hello" > file.txt` | `echo "Linux Rocks!" >> notes.txt` |
| `zcat` | Displays compressed `.gz` file content without extracting. | `zcat demo.txt.gz` | `zcat /var/log/syslog.1.gz` |
| `head` | Displays the first lines of a file. | `head -n 5 demo.txt` | `head -5 /etc/passwd` |
| `tail` | Displays the last lines of a file. | `tail -n 5 demo.txt` | `tail -f logfile.log` |
| `nano` | Opens Nano text editor. Save & Exit: `Ctrl+O`, Enter, `Ctrl+X`. | `nano file.txt` | `nano notes.md` |
| `less` / `more` | Views large files one page at a time. Exit with `q`. | `less demo.txt` | `more /etc/passwd` |
| `cp` | Copies files/directories. | `cp demo.txt ycis/` | `cp -r bca/ ycis/` |
| `mv` | Moves or renames files. | `mv demo.txt ../ycis/` | `mv ycis/ ycis_bca/` |
| `wc` | Counts words, lines, characters in a file. | `wc demo.txt` | `wc -l file.txt` |
| `ln -s` | Creates symbolic link. | `ln -s /path/to/demo.txt softlink-file` | `ln -s /var/log/syslog loglink` |
| `cut -b` | Cuts specific byte/character positions. | `cut -b 1-3 demo.txt` | `echo "Hello" | cut -b 1-2` |
| `tee` | Saves output to file & prints it. | `echo "hi" | tee bvoc.txt` | `ls | tee list.txt` |
| `sort` | Sorts lines in files. | `sort demo.txt` | `sort -r demo.txt` |
| `diff` | Compares two files line by line. | `diff file1.txt file2.txt` | `diff <(echo a) <(echo b)` |
| `vim` | Opens Vim editor. Exit: `Esc`, `:wq` or `:q!`. | `vim file.txt` | `vim notes.md` |
| `df` | Shows disk space usage. | `df -h` | `df /home` |
| `ps` | Displays running processes. | `ps` | `ps aux` |
| `fuser` | Identifies processes using files/sockets. | `fuser demo.txt` | `fuser -v /dev/sda1` |
| `nohup` | Runs a command immune to hangups. | `nohup df -h` | `nohup sleep 60 &` |
| `head -n` | Shows first N lines of a file. | `head -n 5 nohup.out` | `head -n 3 file.txt` |
| `vmstat` | Reports virtual memory statistics. | `vmstat` | `vmstat 2 5` |

---

## 💡 Usage Notes

- **Command Syntax**: Most commands can be modified with **flags** for more control.  
  Example:  
  ```bash
  ls -l       # Long listing format
  head -n 10  # Show first 10 lines
