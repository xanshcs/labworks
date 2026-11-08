# Lab 4 — Partition, mirror, fail, recover

**Pair:** [Your name] / [Partner's name]  
**Driver first half:** [Your name]  
**Machine:** Windows 11 VM / Ubuntu Server VM  
**Date:** 08.11.2026

## What I did

### Windows

1. Checked the partition style of Disk 0 and confirmed that it uses GPT.
2. Created a new partition on the additional 2 GB disk.
3. Formatted the partition and assigned drive letter `E:`.
4. Verified the partition style and disk configuration.

**Why GPT?**

Disk 0 uses GPT because the system boots in UEFI mode. GPT was also selected for the new disk because it is a modern partitioning standard that supports disk capacities larger than 2 TB and avoids the limitations of MBR.

### Linux

1. Checked the initial disk layout using `lsblk`.
2. Identified three additional 2 GB disks: `/dev/sdb`, `/dev/sdc`, and `/dev/sdd`.
3. Partitioned two disks and configured them as RAID 1 members.
4. Created the software RAID array `/dev/md0`.
5. Formatted the array with the ext4 filesystem.
6. Mounted the array at `/mnt/mirror`.
7. Created test files inside the mirror and recorded their SHA-256 checksums.
8. Failed one RAID member (`/dev/sdc1`) to simulate a disk failure.
9. Checked that the filesystem remained accessible and verified the checksums again.
10. Added the third disk (`/dev/sdd1`) to replace the failed RAID member and rebuilt the array.

## Result

### 1. Windows disk configuration

| Property | Value |
|---|---|
| Disk path | `\\?\physicaldisk1` |
| Partition style | GPT |
| Total size | 2 GB |
| Drive letter | E: |
| Partition number | 1 |
| Partition size | 2 GB |
| Partition type | Basic |

### 2. Linux disk layout before configuration

The initial system contained three additional 2 GB disks without partitions.

```text
NAME                       SIZE TYPE FSTYPE      MOUNTPOINT
sda                         20G disk
├─sda1                       1M part
├─sda2                     1.8G part ext4        /boot
└─sda3                    18.2G part LVM2_member
  └─ubuntu--vg-ubuntu--lv   10G lvm  ext4        /
sdb                          2G disk
sdc                          2G disk
sdd                          2G disk
```

### 3. RAID 1 healthy state

The first RAID 1 array was created using `/dev/sdb1` and `/dev/sdc1`.

- RAID level: RAID 1
- Array device: `/dev/md0`
- Filesystem: ext4
- Mount point: `/mnt/mirror`
- State: Clean
- Active devices: 2
- Failed devices: 0

The output showed `[2/2] [UU]`, confirming that both RAID members were active.

### 4. Checksum verification before and after failure

Two test files were stored in `/mnt/mirror`:

| File | SHA-256 checksum |
|---|---|
| `proof.txt` | `a06354e89000b381bca3389db024841c1469eda9cd640d5691a23bfe3f2116b8` |
| `random.bin` | `7dfe74f9d8c21d4282a197438796d3070d326f50e78ef69f9623ab9cea3b384d` |

The checksums were identical before and after the disk failure, confirming that the test files remained intact.

### 5. RAID 1 degraded state

The disk `/dev/sdc1` was marked as faulty to simulate a disk failure.

- RAID level: RAID 1
- Active devices: 1
- Failed devices: 1
- Remaining active disk: `/dev/sdb1`
- Array state: Clean, degraded

The output showed `[2/1] [U_]`, indicating that one RAID member was still working while the other had failed.

Despite the failure, `/mnt/mirror` remained accessible, and both test files passed checksum verification.

### 6. RAID 1 rebuilt state

The third disk, `/dev/sdd1`, was added to replace the failed member.

After the rebuild:

- RAID level: RAID 1
- Active devices: 2
- Working devices: 2
- Failed devices: 0
- Active members: `/dev/sdb1` and `/dev/sdd1`
- Array state: Clean

The output showed `[2/2] [UU]`, confirming that the RAID 1 array had returned to a healthy state.

### 7. RAID 1 question

**Question:** Your colleague deleted the wrong file from the mirror an hour ago. Does RAID 1 help? Why?

No, RAID 1 does not protect against accidental file deletion because changes are immediately replicated across all active disks in the array. When a file is deleted, the deletion is also replicated to the other mirror disk, so the file disappears from both copies. Regular backups or filesystem snapshots are needed to recover accidentally deleted files.

## What did not work the first time

[Describe one actual problem you encountered during the lab, what caused it, and how you fixed it.]

## Evidence

- `evidence/lsblk-before.txt` — shows the initial Linux disk layout before partitioning and RAID configuration.
- `evidence/array-healthy.txt` — proves that the RAID 1 array was initially healthy with two active disks.
- `evidence/checksum-before.txt` — contains the SHA-256 checksums of the test files before the disk failure.
- `evidence/array-degraded.txt` — shows the RAID 1 array after `/dev/sdc1` failed.
- `evidence/checksum-after-failure.txt` — confirms that the test files retained their original checksums after the disk failure.
- `evidence/array-rebuilt.txt` — proves that the array was rebuilt successfully using `/dev/sdd1` and returned to a healthy state.
