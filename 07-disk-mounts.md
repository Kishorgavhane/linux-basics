# Disk & Mounts for DevOps

Disks are quiet.
They don’t complain.
They just fill up… and then everything stops working.

This file helps you understand **how Linux storage actually works**,
so disk issues stop feeling scary and start feeling logical.

---

## What “Disk” Means in Linux

In Linux:
- Disks provide storage
- Storage is attached to the system using **mounts**
- Applications never talk to disks directly
- They talk to **directories**


---

## Disk vs Directory

A disk is **not useful** until it is mounted.

Example:
- Disk exists → but not mounted → system can’t use it
- Disk mounted → attached to a directory → usable

In Linux:
> **Disks are mounted on directories**

---

## Step 1: Seeing Available Disks

Check disks:
```bash
lsblk
```

This shows:
- disk names
- partitions
- mount points (if any)

Read it slowly.
This command answers:

> “What storage does my system have?”

# Understanding Common Disk Names

You may see:
- sda, sdb → physical/virtual disks
- sda1, sda2 → partitions
- nvme0n1 → NVMe disks (cloud systems)

The name is less important than:
- size
- mount point

# Understanding Mount Points

Check mounted filesystems:
```bash
df -h
```

This shows:
- which disk is mounted
- where it is mounted
- how much space is used

This command answers:
> “Where is my data actually going?”

# Why Mount Points Matter in DevOps

Applications write data to directories like:
- /var
- /var/lib
- /data
- /mnt

If these directories are on the wrong disk,
you get:
- disk full issues
- performance issues
- unexpected outages3

Root (/) Disk – The Most Sensitive One

The root filesystem (/) contains:
- system files
- configs
- binaries
- logs (often under /var)

If root disk fills up:
- services fail
- SSH may stop working
- system becomes unstable

# Understanding Disk Usage

Check overall usage:
``bash
df -h
```

Check folder usage:
```bash
du -sh /var/*
```

This helps you understand:
- what is consuming space
- where growth is happening

Mounting a Disk
Mounting means:
> “attaching a disk to a directory”

Example:
```bash
mount /dev/sdb1 /data
```

After this:
- /data points to /dev/sdb1
- applications using /data use that disk

# Temporary vs Permanent Mounts

A mount done with mount:
- works until reboot

For permanent mounts:
- entries are added to /etc/fstab

This separation helps engineers:
- test safely
- then make changes permanent

# /etc/fstab (Configuration File for Mounts)

View file:
```bash
cat /etc/fstab
```

This file tells Linux:
- what disks to mount
- where to mount them
- at boot time

It is powerful and should be edited carefully.

# Hands-On Learning

```bash
lsblk
df -h
mount | head
du -sh /var/*
```

# Important Commands

```bash
lsblk        # disk-list
df -h        # disk-usage
du -sh       # folder-size
mount        # current-mounts
umount       # detach-disk
blkid        # disk-uuid
```
