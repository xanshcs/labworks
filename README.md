# Lab 2 Report: Windows Guest and Network

## 1. Network Mode Choice
I used **VMware NAT (VMnet8)** mode for both guests.
- **Requirement:** Both guests must reach each other and the internet.
- **Reason:** VMware NAT meets both requirements as it provides an isolated virtual switch with DHCP/DNS routing for VM-to-VM communication and external internet access.
- **Why not Bridged:** Bridged mode often fails on managed/campus Wi-Fi networks due to MAC address filtering.
- **Why not Host-only:** Host-only mode blocks internet access completely.

## 2. Network Diagram
Internet
   |
[ Host: Windows 11 PC ] (8.0 GB RAM)
   |
( VMware NAT Router ) (gateway 192.168.9.2)
   |
======= Virtual Switch: VMnet8 (NAT) =======
       |                                |
[ lab01 (Ubuntu) ]             [ lab02-win11 (Windows 11) ]
192.168.9.129                  192.168.9.130
3. Addresses on Both Guests
Ubuntu (lab01): 192.168.9.129

Windows 11 (lab02-win11): 192.168.9.130

4. Firewall Configuration
Initial Failure: Linux to Windows ping failed initially because Windows Defender Firewall treats unknown virtual networks under the Public profile and drops incoming ICMP Echo Requests by default.

Fix: Added a specific inbound firewall rule via PowerShell:
New-NetFirewallRule -DisplayName "Lab02 - allow ping (ICMPv4 echo)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -RemoteAddress LocalSubnet -Action Allow

5. Overcommitment Experiment
Host Total RAM: 8.0 GB DDR4

Allocated Memory:

Ubuntu (lab01): 4 GB

Windows 11 (lab02-win11): 6 GB

Total Promised: 10 GB (Ratio: ~1.25x / 125% of Host RAM)

Observations:

Before load (evidence/host-memory-before.png): Host memory usage was 5.7 GB (74%), Committed memory was 12.0 GB.

After load (evidence/host-memory-after.png): Host memory usage reached 7.4 GB (96%), and Committed memory spiked to 24.3 GB, indicating heavy swapping/paging to the host SSD.

Hypervisor Behavior: VMware initially blocked starting the second VM with a physical memory error until memory swapping was explicitly enabled in VMware Preferences.

6. Post-Experiment Restoration
Memory allocations were returned to sane values:

Ubuntu (lab01): 2 GB

Windows 11 (lab02-win11): 4 GB
