Markdown
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
Linux layout — before
Plaintext
NAME                       SIZE TYPE FSTYPE      MOUNTPOINT
loop0                     66.8M loop squashfs    /snap/core24/2124
loop1                     50.1M loop squashfs    /snap/snapd/27710
loop2                     66.8M loop squashfs    /snap/core24/1643
loop3                      1.5M loop squashfs    /snap/hwctl/123
loop4                      1.5M loop squashfs    /snap/hwctl/131
sda                         20G disk             
├─sda1                       1M part             
├─sda2                    1.8G part ext4        /boot
└─sda3                   18.2G part LVM2_member 
  └─ubuntu--vg-ubuntu--lv   10G lvm  ext4        /
sdb                          2G disk             
sdc                          2G disk             
sdd                          2G disk             
sr0                        2.7G rom  iso9660     
Linux layout — after the rebuild
Plaintext
NAME                      SIZE TYPE FSTYPE      MOUNTPOINT
sda                        20G disk             
├─sda1                      1M part             
├─sda2                    1.8G part ext4        /boot
└─sda3                   18.2G part LVM2_member 
  └─ubuntu--vg-ubuntu--lv  10G lvm  ext4        /
sdb                         2G disk             
└─sdb1                      2G part raid        
  └─md0                     2G ext4         /mnt/mirror
sdc                         2G disk             
└─sdc1                      2G part raid        
sdd                         2G disk             
└─sdd1                      2G part raid        
  └─md0                     2G ext4         /mnt/mirror
Role	Device
Mirror half A	sdb1
Failed half	sdc1
Replacement	sdd1
The question
Your colleague deleted the wrong file from the mirror an hour ago. Does RAID 1 help? Why?

No, RAID 1 does not help because a mirror instantly replicates every write and deletion across all active disks in the array. Since the deletion command is treated as a normal write operation, the file is simultaneously removed from both halves of the mirror. A proper backup or snapshot history would have helped restore the deleted file instead.
