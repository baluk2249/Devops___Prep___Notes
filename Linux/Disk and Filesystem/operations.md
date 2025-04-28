# 📂 Disk and Filesystem

## 1. Understanding Linux Filesystem Hierarchy
- `/` : Root directory
- `/home` : User files
- `/etc` : Configuration files
- `/var` : Variable data (logs, spool files)
- `/usr` : User programs and data
- `/tmp` : Temporary files

---

## 2. Disk and Partition Management

### List All Disks and Partitions
```bash
lsblk
fdisk -l
```

### Creating and Managing Partitions

#### Create New Partition
```bash
sudo fdisk /dev/sdX
```
- `n` → new partition
- `w` → write changes

#### View Partition Table
```bash
sudo parted /dev/sdX print
```

---

## 3. Filesystem Creation

### Create Filesystem
```bash
sudo mkfs.ext4 /dev/sdX1
```
> Creates ext4 filesystem.

### Other Filesystem Types
- `mkfs.xfs`
- `mkfs.vfat`
- `mkfs.ntfs`

### Check Filesystem Type
```bash
sudo blkid /dev/sdX1
```

---

## 4. Mounting and Unmounting

### Mount a Filesystem
```bash
sudo mount /dev/sdX1 /mnt
```

### Unmount a Filesystem
```bash
sudo umount /mnt
```

### Mount on Boot (Persistent)
Edit `/etc/fstab`:
```bash
/dev/sdX1  /mnt  ext4  defaults  0  2
```

---

## 5. Checking Disk Usage

### Show Disk Space Usage
```bash
df -h
```

### Show Directory Sizes
```bash
du -sh *
```

---

## 6. Filesystem Checking and Repair

### Check Filesystem
```bash
sudo fsck /dev/sdX1
```

### Force Check
```bash
sudo fsck -f /dev/sdX1
```

---

## 7. Logical Volume Management (LVM)

### Basic LVM Terms
- **PV** (Physical Volume)
- **VG** (Volume Group)
- **LV** (Logical Volume)
 
### Create LVM Setup
```bash
sudo pvcreate /dev/sdX1
sudo vgcreate my_vg /dev/sdX1
sudo lvcreate -L 10G -n my_lv my_vg
sudo mkfs.ext4 /dev/my_vg/my_lv
sudo mount /dev/my_vg/my_lv /mnt
```

### Extend Logical Volume
```bash
sudo lvextend -L +5G /dev/my_vg/my_lv
sudo resize2fs /dev/my_vg/my_lv
```

---

## 8. Disk and Partition Backup

### Using `dd`
```bash
sudo dd if=/dev/sdX of=/path/to/backup.img bs=4M
```

### Restore with `dd`
```bash
sudo dd if=/path/to/backup.img of=/dev/sdX
```

---

## 9. Useful Disk Utilities

| Utility | Purpose |
|:-------|:--------|
| `lsblk` | List information about block devices |
| `fdisk` | Partition table manipulator |
| `parted` | Manage partitions |
| `mkfs` | Create filesystems |
| `fsck` | Filesystem check and repair |
| `mount/umount` | Mount and unmount filesystems |
| `lvm` | Logical Volume Manager tools |
| `df/du` | Disk space and usage |
| `dd` | Backup and cloning |

---

# 🔥 Pro Tip:
> Always **backup critical data** before manipulating disks or partitions!

---


