# Linux-for-DevOps

# Day 01 – Linux Basics

## 📌 Introduction
This document is part of a learning series for mastering **Linux**.  
In this first module, we will cover:
- The difference between UNIX and Linux
- Linux system architecture
- Hardware commands in Linux
- Process states in Linux
- Practical commands with examples

Whether you are a beginner or brushing up your skills, this guide provides both theoretical and practical knowledge.

---

## 1. Difference Between UNIX and Linux

| Feature         | UNIX                                      | Linux                                        |
|-----------------|-------------------------------------------|----------------------------------------------|
| **Origin**      | Developed in 1969 at AT&T Bell Labs       | Developed in 1991 by Linus Torvalds          |
| **License**     | Proprietary (paid licensing)              | Open-source under GNU GPL                    |
| **Usage**       | Servers, mainframes, workstations         | Servers, desktops, embedded systems, mobile |
| **Portability** | Limited portability                       | Highly portable (multiple distributions)     |
| **Examples**    | AIX, HP-UX, Solaris                        | Ubuntu, Red Hat, Debian, Arch, etc.          |

---

## 2. Linux System Architecture

Linux is composed of several layers:

1. **Hardware Layer**  
   - Physical components: CPU, RAM, disks, network cards.

2. **Kernel Layer**  
   - Core of the OS; manages hardware, processes, and system calls.  
   - Key components:
     - Process Manager
     - Memory Manager
     - File System
     - Device Drivers

3. **System Call Interface**  
   - The bridge between user applications and the kernel.

4. **Shell**  
   - Command interpreter (e.g., `bash`, `zsh`).

5. **Application Layer**  
   - User programs (editors, compilers, browsers, etc.).

---

## 3. Hardware Commands in Linux

| Command              | Description                        | Example & Usage |
|----------------------|------------------------------------|-----------------|
| `lscpu`              | Display CPU architecture info      | `lscpu` |
| `lsblk`              | List block devices (disks, partitions) | `lsblk -f` |
| `lshw`               | List hardware info                 | `sudo lshw -short` |
| `free -h`            | Show memory usage                  | `free -h` |
| `df -h`              | Show disk usage                    | `df -h` |
| `inxi -Fx`           | Detailed system info               | `inxi -Fx` |
| `lspci`              | Show PCI devices                   | `lspci` |
| `lsusb`              | Show USB devices                   | `lsusb` |
| `dmidecode`          | Show BIOS/system details           | `sudo dmidecode` |

---

## 4. States of Processes in Linux

| Code | State Name                  | Description |
|------|-----------------------------|-------------|
| **R** | Running                    | Running or ready to run |
| **S** | Sleeping (Interruptible)   | Waiting for an event, can be interrupted |
| **D** | Sleeping (Uninterruptible) | Waiting for I/O, cannot be interrupted |
| **T** | Stopped                    | Process stopped by signal/debugger |
| **Z** | Zombie                     | Process finished but not cleaned by parent |
| **X** | Dead                       | Terminated (not normally visible) |
| **I** | Idle                       | Kernel thread idle state |

**Check process states:**
```bash
ps aux
top
htop




