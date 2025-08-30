# 🖥️ Linux Volume Management (LVM) Cheat Sheet

## 🔹 Key Concepts
- **PV (Physical Volume):** Actual disk/partition prepared for LVM (e.g., `/dev/sdb1`).
- **VG (Volume Group):** Pool of storage created from PVs.
- **LV (Logical Volume):** Flexible partitions created from a VG.
- **PE (Physical Extent):** Smallest storage unit in LVM.

---

## 🔹 Physical Volume (PV) Commands
```bash
# Create a physical volume
pvcreate /dev/sdb1

# Display detailed info about PVs
pvdisplay

# List all PVs (summary)
pvs

# Remove PV from LVM
pvremove /dev/sdb1
```

---

## 🔹 Volume Group (VG) Commands
```bash
# Create a volume group
vgcreate myvg /dev/sdb1 /dev/sdc1

# Extend VG by adding new PV
vgextend myvg /dev/sdd1

# Reduce VG by removing PV
vgreduce myvg /dev/sdd1

# Display detailed info about VG
vgdisplay

# List all VGs (summary)
vgs

# Remove VG
vgremove myvg
```

---

## 🔹 Logical Volume (LV) Commands
```bash
# Create a logical volume of 5GB
lvcreate -L 5G -n mylv myvg

# Extend LV by 2GB
lvextend -L +2G /dev/myvg/mylv
resize2fs /dev/myvg/mylv   # Resize filesystem after extend

# Reduce LV to 3GB (Unmount before reducing!)
lvreduce -L 3G /dev/myvg/mylv
resize2fs /dev/myvg/mylv

# Display detailed info about LVs
lvdisplay

# List all LVs (summary)
lvs

# Remove LV
lvremove /dev/myvg/mylv
```

---

## 🔹 Snapshots
```bash
# Create a snapshot of LV (1GB size)
lvcreate -L 1G -s -n mysnap /dev/myvg/mylv

# Remove snapshot
lvremove /dev/myvg/mysnap
```

---

## 🔹 Other Useful Commands
```bash
# Scan for LVM devices
lvmdiskscan

# Activate/Deactivate an LV
lvchange -ay /dev/myvg/mylv   # activate
lvchange -an /dev/myvg/mylv   # deactivate

# Check LVM version
lvm version
```

---

## 🔹 Example Workflow
```bash
# Step 1: Initialize disk for LVM
pvcreate /dev/sdb1

# Step 2: Create a volume group
vgcreate myvg /dev/sdb1

# Step 3: Create a logical volume
lvcreate -L 10G -n mydata myvg

# Step 4: Format the LV with ext4 filesystem
mkfs.ext4 /dev/myvg/mydata

# Step 5: Mount it
mkdir /mnt/mydata
mount /dev/myvg/mydata /mnt/mydata
```
