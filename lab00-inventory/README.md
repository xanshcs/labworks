# Lab 0 - Inventory

| What | Value | Where I got it |
|---|---|---|
| CPU model | 11th Gen Intel(R) Core(TM) i5-11400H @ 2.70GHz | Get-CimInstance Win32_Processor |
| Cores / threads | 6 / 12 | Get-CimInstance Win32_Processor |
| RAM total | 8 GB | Get-CimInstance Win32_PhysicalMemory |
| RAM modules / speed | 1 1 module(s), 3200 MHz | Get-CimInstance Win32_PhysicalMemory |
| Disk model / type | NVMe SAMSUNG MZVLQ512HBLU-00B00, SSD, NVMe | Get-PhysicalDisk |
| Free space on VM volume (C:) | 88 GB | Get-Volume -DriveLetter C |
| Firmware type / version / date | Uefi, FX506HE.311, 08/12/2022 05:00:00 | Get-ComputerInfo, Win32_BIOS |
| Hardware virtualization enabled | True | Win32_Processor, Win32_ComputerSystem (HypervisorPresent) |

## Virtualization
VirtualizationFirmwareEnabled=True, HypervisorPresent=False.

## What did not work
ВПИШИ СЮДА СВОЮ НАСТОЯЩУЮ ОШИБКУ (что не получилось и как исправила)

