# 🗄️ Linux Volume Management (LVM) - Complete Guide

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Documentation](https://img.shields.io/badge/docs-complete-brightgreen)](https://github.com/user/linux-volume-management)
[![Linux](https://img.shields.io/badge/OS-Linux-blue.svg)](https://www.linux.org/)
[![LVM](https://img.shields.io/badge/LVM-2.x-orange.svg)](https://sourceware.org/lvm2/)
[![Shell](https://img.shields.io/badge/Shell-Bash-green.svg)](https://www.gnu.org/software/bash/)

> **Comprehensive guide to Linux Logical Volume Manager (LVM) with practical examples, commands, and best practices for dynamic storage management.**

---

## 📋 Table of Contents

- [🌟 Features](#-features)
- [⚡ Quick Start](#-quick-start)
- [🏗️ LVM Architecture](#️-lvm-architecture)
- [📚 Core Concepts](#-core-concepts)
- [🔧 Commands Reference](#-commands-reference)
- [💡 Examples](#-examples)
- [⚠️ Best Practices](#️-best-practices)
- [🔍 Troubleshooting](#-troubleshooting)
- [📖 Advanced Topics](#-advanced-topics)
- [🤝 Contributing](#-contributing)

---

## 🌟 Features

- **Dynamic Storage Management** - Resize volumes without downtime
- **Multi-Device Support** - Span volumes across multiple disks
- **Snapshots** - Point-in-time backups for safe operations
- **High Flexibility** - Easy migration and reorganization
- **Fault Tolerance** - Better error handling than traditional partitioning

## ⚡ Quick Start

### Prerequisites

```bash
# Check if LVM tools are installed
which lvm
sudo pvs --version

# Install LVM tools (if needed)
# Ubuntu/Debian
sudo apt update && sudo apt install lvm2

# RHEL/CentOS/Fedora
sudo yum install lvm2
# or
sudo dnf install lvm2
```

### Basic LVM Setup (5 Minutes)

```bash
# 1. Create Physical Volume
sudo pvcreate /dev/sdb1

# 2. Create Volume Group  
sudo vgcreate myvg /dev/sdb1

# 3. Create Logical Volume
sudo lvcreate -L 10G -n mylv myvg

# 4. Create filesystem
sudo mkfs.ext4 /dev/myvg/mylv

# 5. Mount it
sudo mkdir /mnt/data
sudo mount /dev/myvg/mylv /mnt/data
```

## 🏗️ LVM Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    LVM Architecture                     │
├─────────────────────────────────────────────────────────┤
│  Applications & Users                                   │
├─────────────────────────────────────────────────────────┤
│  Mount Points:    /home    /var     /data              │
├─────────────────────────────────────────────────────────┤
│  Filesystems:    [ext4]   [xfs]   [ext4]              │
├─────────────────────────────────────────────────────────┤
│  Logical Volumes: [homelv] [varlv] [datalv]            │
├─────────────────────────────────────────────────────────┤
│  Volume Group:    [        datavg        ]             │
├─────────────────────────────────────────────────────────┤
│  Physical Volumes: [PV1]    [PV2]    [PV3]             │
├─────────────────────────────────────────────────────────┤
│  Physical Storage: /dev/sdb1 /dev/sdc1 /dev/sdd        │
└─────────────────────────────────────────────────────────┘
```

## 📚 Core Concepts

### Physical Volumes (PV) 🏠
- **Real storage devices** (disks, partitions)
- Foundation layer of LVM
- Cannot exceed physical hardware limits

### Volume Groups (VG) 🏢
- **Storage pools** combining multiple PVs
- Aggregates space from multiple physical devices
- Can be extended by adding more PVs

### Logical Volumes (LV) 🏠🏠
- **Virtual partitions** created from VG space
- Where filesystems are actually created
- Can be resized dynamically

## 🔧 Commands Reference

### Physical Volume Management

<details>
<summary><b>📦 PV Commands</b></summary>

```bash
# Create Physical Volumes
sudo pvcreate /dev/sdb1                    # Single PV
sudo pvcreate /dev/sdb1 /dev/sdc1         # Multiple PVs

# View Physical Volumes
sudo pvs                                   # Summary view
sudo pvdisplay                            # Detailed view
sudo pvdisplay /dev/sdb1                  # Specific PV

# Management
sudo pvmove /dev/sdb1 /dev/sdc1           # Move data between PVs
sudo pvremove /dev/sdb1                   # Remove PV (must be unused)
sudo pvscan                               # Scan for PVs
```

</details>

### Volume Group Management

<details>
<summary><b>🗃️ VG Commands</b></summary>

```bash
# Create Volume Groups
sudo vgcreate datavg /dev/sdb1            # Single PV
sudo vgcreate datavg /dev/sdb1 /dev/sdc1  # Multiple PVs

# View Volume Groups
sudo vgs                                   # Summary view
sudo vgdisplay                            # Detailed view
sudo vgdisplay datavg                     # Specific VG

# Extend/Reduce
sudo vgextend datavg /dev/sdd1            # Add PV to VG
sudo vgreduce datavg /dev/sdd1            # Remove PV from VG

# Management
sudo vgchange -a y datavg                 # Activate VG
sudo vgchange -a n datavg                 # Deactivate VG
sudo vgrename oldvg newvg                 # Rename VG
```

</details>

### Logical Volume Management

<details>
<summary><b>💾 LV Commands</b></summary>

```bash
# Create Logical Volumes
sudo lvcreate -L 20G -n homelv datavg     # Fixed size
sudo lvcreate -l 50%VG -n varlv datavg    # Percentage of VG
sudo lvcreate -l 100%FREE -n datalv datavg # All remaining space

# View Logical Volumes
sudo lvs                                   # Summary view
sudo lvdisplay                            # Detailed view
sudo lvdisplay /dev/datavg/homelv         # Specific LV

# Resize Operations
sudo lvextend -L +5G /dev/datavg/homelv   # Extend by 5GB
sudo lvextend -L 30G /dev/datavg/homelv   # Extend to 30GB
sudo lvextend -L +5G -r /dev/datavg/homelv # Extend + resize filesystem

# Management
sudo lvchange -a y /dev/datavg/homelv     # Activate LV
sudo lvrename datavg homelv newhome       # Rename LV
```

</details>

### Filesystem Operations

<details>
<summary><b>🗂️ Filesystem Commands</b></summary>

```bash
# Create Filesystems
sudo mkfs.ext4 /dev/datavg/homelv         # ext4
sudo mkfs.xfs /dev/datavg/varlv           # XFS
sudo mkfs.ext4 -L "Home" /dev/datavg/homelv # With label

# Mount Operations
sudo mount /dev/datavg/homelv /home       # Mount
sudo umount /home                         # Unmount

# Resize Filesystems
sudo resize2fs /dev/datavg/homelv         # ext4 (after LV resize)
sudo xfs_growfs /home                     # XFS (must be mounted)
```

</details>

## 💡 Examples

### Example 1: Web Server Setup

<details>
<summary><b>🌐 Complete Web Server LVM Setup</b></summary>

```bash
#!/bin/bash
# Web Server LVM Setup Script

set -e  # Exit on any error

echo "🚀 Setting up LVM for Web Server..."

# Step 1: Prepare disks (assuming /dev/sdb, /dev/sdc available)
echo "📦 Creating Physical Volumes..."
sudo pvcreate /dev/sdb /dev/sdc

# Step 2: Create Volume Group
echo "🗃️ Creating Volume Group..."
sudo vgcreate webvg /dev/sdb /dev/sdc

# Step 3: Create Logical Volumes
echo "💾 Creating Logical Volumes..."
sudo lvcreate -L 20G -n rootlv webvg      # OS files
sudo lvcreate -L 50G -n weblv webvg       # Web content  
sudo lvcreate -L 30G -n dblv webvg        # Database
sudo lvcreate -L 20G -n loglv webvg       # Logs
sudo lvcreate -l 100%FREE -n backuplv webvg # Remaining space

# Step 4: Create Filesystems
echo "🗂️ Creating Filesystems..."
sudo mkfs.ext4 -L "WebData" /dev/webvg/weblv
sudo mkfs.ext4 -L "Database" /dev/webvg/dblv
sudo mkfs.ext4 -L "Logs" /dev/webvg/loglv
sudo mkfs.xfs -L "Backup" /dev/webvg/backuplv

# Step 5: Create mount points and mount
echo "🔗 Setting up mount points..."
sudo mkdir -p /var/www /var/lib/mysql /var/log/apps /backup

sudo mount /dev/webvg/weblv /var/www
sudo mount /dev/webvg/dblv /var/lib/mysql
sudo mount /dev/webvg/loglv /var/log/apps
sudo mount /dev/webvg/backuplv /backup

# Step 6: Update fstab for persistence
echo "📝 Updating /etc/fstab..."
cat << EOF | sudo tee -a /etc/fstab
# LVM Web Server Mounts
/dev/webvg/weblv    /var/www        ext4  defaults  0  2
/dev/webvg/dblv     /var/lib/mysql  ext4  defaults  0  2  
/dev/webvg/loglv    /var/log/apps   ext4  defaults  0  2
/dev/webvg/backuplv /backup         xfs   defaults  0  2
EOF

echo "✅ Web Server LVM Setup Complete!"
echo "📊 Current Status:"
sudo pvs && echo "---" && sudo vgs && echo "---" && sudo lvs
df -h | grep "/dev/mapper"
```

</details>

### Example 2: Dynamic Expansion

<details>
<summary><b>📈 Adding Storage and Expanding Volumes</b></summary>

```bash
#!/bin/bash
# Dynamic Storage Expansion Example

echo "📈 Expanding storage dynamically..."

# Scenario: Database volume is running out of space
echo "Current database volume usage:"
df -h /var/lib/mysql

# Method 1: Extend existing LV (if VG has free space)
FREE_SPACE=$(sudo vgdisplay webvg | grep "Free" | awk '{print $7}')
if [[ "$FREE_SPACE" > "0.00" ]]; then
    echo "🔧 Extending from available VG space..."
    sudo lvextend -L +10G -r /dev/webvg/dblv
else
    echo "📦 Adding new disk to expand storage..."
    
    # Method 2: Add new disk and extend VG
    sudo pvcreate /dev/sdd
    sudo vgextend webvg /dev/sdd
    
    # Now extend the logical volume
    sudo lvextend -L +20G -r /dev/webvg/dblv
fi

echo "✅ Database volume expanded!"
echo "📊 New usage:"
df -h /var/lib/mysql
sudo lvs webvg
```

</details>

### Example 3: Snapshot Backup

<details>
<summary><b>📸 Creating Snapshots for Backup</b></summary>

```bash
#!/bin/bash
# LVM Snapshot Backup Script

DATE=$(date +%Y%m%d_%H%M%S)
SNAPSHOT_SIZE="5G"
BACKUP_DIR="/backup"

echo "📸 Creating snapshot backup..."

# Create snapshot
echo "Creating snapshot of web data..."
sudo lvcreate -L $SNAPSHOT_SIZE -s -n webdata_snap_$DATE /dev/webvg/weblv

# Mount snapshot
MOUNT_POINT="/mnt/snapshot_$DATE"
sudo mkdir -p $MOUNT_POINT
sudo mount -o ro /dev/webvg/webdata_snap_$DATE $MOUNT_POINT

# Create backup
echo "Creating backup archive..."
sudo tar czf $BACKUP_DIR/webdata_backup_$DATE.tar.gz -C $MOUNT_POINT .

# Cleanup
echo "Cleaning up snapshot..."
sudo umount $MOUNT_POINT
sudo rmdir $MOUNT_POINT
sudo lvremove -f /dev/webvg/webdata_snap_$DATE

echo "✅ Backup complete: $BACKUP_DIR/webdata_backup_$DATE.tar.gz"
ls -lh $BACKUP_DIR/webdata_backup_$DATE.tar.gz
```

</details>

## ⚠️ Best Practices

### 🛡️ Safety Guidelines

- **Always backup** before major operations
- **Test in development** before production changes
- **Leave free space** in volume groups (10-20%)
- **Use meaningful names** for VGs and LVs
- **Monitor disk health** with SMART tools

### 🚀 Performance Tips

```bash
# Create striped LV for better I/O performance
sudo lvcreate -L 20G -i 2 -I 64 -n fastlv datavg /dev/sdb1 /dev/sdc1

# Use appropriate filesystem mount options
sudo mount -o rw,noatime,data=writeback /dev/datavg/fastlv /fast

# Monitor I/O performance
iostat -x 1 5
```

### 📋 Naming Conventions

```bash
# Recommended naming scheme
Volume Group: <purpose>vg    (webvg, datavg, rootvg)
Logical Volume: <function>lv  (homelv, varlv, dblv, loglv)

# Examples
sudo vgcreate webvg /dev/sdb1
sudo lvcreate -L 20G -n appdatalv webvg
sudo lvcreate -L 10G -n apploglv webvg
```

## 🔍 Troubleshooting

### Common Issues and Solutions

<details>
<summary><b>🚨 Volume Group Not Found</b></summary>

```bash
# Scan for volume groups
sudo vgscan --mknodes

# Activate all volume groups
sudo vgchange -a y

# Check LVM configuration
sudo lvmdiskscan
```

</details>

<details>
<summary><b>📉 Cannot Extend Volume</b></summary>

```bash
# Check available space
sudo vgdisplay datavg | grep -E "(Free|Size)"

# If no free space, add new PV
sudo pvcreate /dev/sde1
sudo vgextend datavg /dev/sde1

# Then extend LV
sudo lvextend -L +10G /dev/datavg/mylv
```

</details>

<details>
<summary><b>🔧 Recovery from Missing PV</b></summary>

```bash
# Check for missing PVs
sudo vgs -o +devices

# Remove missing PV from VG
sudo vgreduce --removemissing datavg

# If data was on missing PV, restore from backup
sudo vgcfgbackup datavg      # Create backup first
# sudo vgcfgrestore datavg   # Restore if needed
```

</details>

### 📊 Monitoring Script

<details>
<summary><b>📈 LVM Health Check Script</b></summary>

```bash
#!/bin/bash
# lvm-health-check.sh

echo "=== LVM Health Check ==="
echo "Date: $(date)"
echo

# Check PV health
echo "🏠 Physical Volumes:"
sudo pvs -o pv_name,vg_name,pv_size,pv_free,pv_attr --units h

# Check VG usage
echo -e "\n🗃️ Volume Groups:"
sudo vgs -o vg_name,vg_size,vg_free,vg_attr --units h

# Alert for high usage
echo -e "\n⚠️ Usage Alerts:"
sudo vgs --noheadings --units b -o vg_name,vg_size,vg_free | while read vg size free; do
    used=$((size - free))
    percent=$((used * 100 / size))
    if [ $percent -gt 90 ]; then
        echo "WARNING: Volume Group $vg is ${percent}% full!"
    fi
done

# Check LV status  
echo -e "\n💾 Logical Volumes:"
sudo lvs -o lv_name,vg_name,lv_size,lv_attr --units h

# Filesystem usage
echo -e "\n🗂️ Filesystem Usage:"
df -h | grep "/dev/mapper" | awk '{print $1 "\t" $5 "\t" $6}'
```

</details>

## 📖 Advanced Topics

### Striping and Mirroring

<details>
<summary><b>⚡ Performance Enhancement</b></summary>

```bash
# Striped LV (RAID 0 equivalent)
sudo lvcreate -L 40G -i 2 -I 64 -n stripedlv datavg

# Mirrored LV (RAID 1 equivalent)  
sudo lvcreate -L 20G -m 1 -n mirroredlv datavg

# RAID 5 equivalent
sudo lvcreate --type raid5 -L 60G -i 3 -n raid5lv datavg
```

</details>

### Thin Provisioning

<details>
<summary><b>💰 Space Optimization</b></summary>

```bash
# Create thin pool
sudo lvcreate -L 100G -T datavg/thinpool

# Create thin volumes
sudo lvcreate -V 50G -T datavg/thinpool -n thinlv1
sudo lvcreate -V 50G -T datavg/thinpool -n thinlv2

# Monitor thin pool usage
sudo lvs -o lv_name,lv_size,data_percent datavg
```

</details>

### Migration and Backup

<details>
<summary><b>🔄 Data Migration</b></summary>

```bash
# Migrate LV to different PVs
sudo pvmove --name mylv /dev/sdb1 /dev/sdc1

# Create portable backup
sudo dd if=/dev/datavg/mylv | gzip > /backup/mylv_backup.gz

# Restore from backup  
gunzip -c /backup/mylv_backup.gz | sudo dd of=/dev/newvg/mylv
```

</details>

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### 🐛 Bug Reports
- Use the issue tracker
- Include system information (`uname -a`, `lvm version`)
- Provide steps to reproduce

### 💡 Feature Requests
- Describe the use case
- Explain why it would be useful
- Provide examples if possible

### 📝 Documentation
- Fix typos and grammar
- Add examples for complex scenarios
- Improve clarity of explanations

### 🔧 Code Contributions
- Fork the repository
- Create a feature branch
- Add tests for new functionality
- Ensure all examples work
- Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Linux LVM development team
- Community contributors
- Red Hat for LVM documentation
- Ubuntu/Debian maintainers

## 📞 Support

- 📖 [Official LVM Documentation](https://sourceware.org/lvm2/)
- 🐧 [Linux Documentation Project](https://tldp.org/)
- 💬 [Stack Overflow LVM Tag](https://stackoverflow.com/questions/tagged/lvm)
- 🗨️ [Reddit r/linuxadmin](https://reddit.com/r/linuxadmin)

---

<div align="center">

### ⭐ Star this repository if it helped you!

**Made with ❤️ for the Linux community**

[⬆️ Back to Top](#️-linux-volume-management-lvm---complete-guide)

</div>