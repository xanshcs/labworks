# Lab 4 — Storage

## Windows
Disk 0: partition style GPT, firmware_type UEFI — because the system booted in UEFI mode which requires a GPT partition table.
New disk: partition style GPT — because it supports modern standards, sizes well beyond 2 TB, and has no legacy MBR limitations.


DiskPath            : \\?\physicaldisk1
PartitionStyle      : GPT
TotalSize           : 2 GB
---
DriveLetter         : E
PartitionNumber     : 1
Size                : 2 GB
Type                : Basic

NAME                      SIZE TYPE FSTYPE      MOUNTPOINT
sda                        20G disk
├─sda1                      1M part
├─sda2                      2G part ext4        /boot
└─sda3                     18G part LVM2_member
  └─ubuntu--vg-ubuntu--lv  10G lvm  ext4        /
sdb                         2G disk
sdc                         2G disk
sdd                         2G disk

NAME                      SIZE TYPE FSTYPE      MOUNTPOINT
sda                        20G disk
├─sda1                      1M part
├─sda2                      2G part ext4        /boot
└─sda3                     18G part LVM2_member
  └─ubuntu--vg-ubuntu--lv  10G lvm  ext4        /
sdb                         2G disk
└─sdb1                      2G part linux_raid_member
  └─md0                     2G part ext4        /mnt/mirror
sdc                         2G disk
└─sdc1                      2G part linux_raid_member
sdd                         2G disk
└─sdd1                      2G part linux_raid_member
  └─md0                     2G part ext4        /mnt/mirror

RoleDeviceMirror half Asdb1Failed halfsdc1Replacementsdd1

The question
Your colleague deleted the wrong file from the mirror an hour ago. Does RAID 1 help? Why?
No, RAID 1 does not help in this situation because a mirror synchronously replicates every write and deletion across all active disks in real time. Therefore, deleting a file propagates instantly to all copies within the array, destroying the data everywhere simultaneously. A proper separate data backup or filesystem snapshot taken prior to the deletion is required to recover the lost file.
