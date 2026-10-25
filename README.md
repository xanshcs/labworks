# Lab 2 Report: Windows Guest and Network

## 1. Network Mode Choice & Analysis
I used **VMware NAT (VMnet8)** mode for both guests.

### Requirements & Evaluation of Modes:
- **Requirement:** Both guests must reach each other (VM-to-VM communication) and have external access to the internet.
- **Why VMware NAT meets the requirement:** VMware NAT creates an isolated virtual switch (`VMnet8`) with an embedded DHCP server and DNS router (gateway). This allows both virtual machines to assign local IPv4 addresses in the same `/24` subnet while sharing the host's physical internet connection.
- **Why not Bridged Mode:** Bridged mode places the VMs directly on the physical network. On campus or corporate Wi-Fi networks, MAC address filtering often silently drops unknown guest virtual MAC addresses, resulting in complete network failure (no DHCP IP assignment).
- **Why not Host-Only Mode:** Host-only mode completely isolates the virtual switch from any external network adapters, which fails the requirement for internet connectivity.

---

## 2. Network Diagram

                       [ Internet (8.8.8.8) ]
                                 |
                     [ Physical Host PC ] 
                  (Windows 11, 8.0 GB RAM)
                                 |
                 ( VMware NAT Gateway: 192.168.9.2 )
                                 |
======== Virtual Switch: VMnet8 (NAT Subnet: 192.168.9.0/24) ========
        |                                                 |
[ lab01 (Ubuntu Server) ]                       [ lab02-win11 (Windows 11) ]
Interface: ens33                                Interface: Ethernet0
IP: 192.168.9.129/24                            IP: 192.168.9.130/24

3. Guest Network Configuration
Both virtual machines were assigned addresses via VMware's internal DHCP server within the same subnet (192.168.9.0/24):

Ubuntu Guest (lab01): 192.168.9.129 (Interface: ens33)

Windows 11 Guest (lab02-win11): 192.168.9.130 (Interface: Ethernet0)

4. ICMP Ping & Firewall Rule Configuration
Initial Network Behavior:
Windows → Linux Ping: Worked immediately. Ubuntu Server has no restrictive default firewall rules blocking incoming ICMP Echo Requests.

Linux → Windows Ping: Failed with 100% packet loss.

Reason: Windows Defender Firewall automatically detects unknown virtual networks and places them under the Public Network Profile (Get-NetConnectionProfile). Under the Public profile, Windows drops all incoming ICMP Echo Requests (ping packets) by default as a security precaution.

Specific Rule Implementation:
To fix connectivity without compromising security, I created a targeted inbound firewall rule via PowerShell (run as Administrator) instead of disabling the firewall or opening unnecessary file-sharing protocols:

PowerShell
New-NetFirewallRule -DisplayName "Lab02 - allow ping (ICMPv4 echo)" `
                    -Direction Inbound `
                    -Protocol ICMPv4 `
                    -IcmpType 8 `
                    -RemoteAddress LocalSubnet `
                    -Action Allow
Rule Parameters Explained:

-Direction Inbound: Applies strictly to incoming traffic.

-Protocol ICMPv4 -IcmpType 8: Restricts allowed traffic strictly to ICMP Echo Requests (ping).

-RemoteAddress LocalSubnet: Restricts access only to devices within the local virtual subnet (192.168.9.0/24), blocking any external networks.

-Action Allow: Permits only matching packets through.

5. Memory Overcommitment Experiment
Premise & Baseline Configuration:
Host Physical RAM: 8.0 GB DDR4

Baseline Allocations (Sane):

Ubuntu (lab01): 2.0 GB

Windows 11 (lab02-win11): 4.0 GB

Total Sane Promised: 6.0 GB (Leaving ~2.0 GB for Host OS)

Overcommit Setup:
Memory allocations were intentionally raised to test hypervisor page swapping and host behavior under memory stress:

Ubuntu (lab01): Raised to 4.0 GB

Windows 11 (lab02-win11): Raised to 6.0 GB

Total Promised RAM: 10.0 GB (~125% / 1.25x overcommit ratio relative to physical 8.0 GB RAM)

Measurements & Observations:
Metric / State	Before Load (evidence/host-memory-before.png)	After Load (evidence/host-memory-after.png)
Physical Memory Usage	5.7 GB / 7.7 GB (74%)	7.4 GB / 7.7 GB (96%)
Available RAM	~2.0 GB	375 MB
Committed Virtual Memory	12.0 GB / 18.9 GB	24.3 GB / 27.9 GB
System Behavior	Smooth, responsive UI	Heavy host thrashing, laggy input, host active page file swapping
Hypervisor & OS Behavior:
Hypervisor Intervention: VMware Workstation initially threw a physical memory allocation warning upon launching the second VM until host page file swapping was explicitly permitted in Edit → Preferences → Memory.

Workload Generation:

Linux: Executed stress-ng --vm 1 --vm-bytes 90% --vm-keep --timeout 300s to force memory allocation.

Windows: Opened multiple heavy built-in applications and array allocations in PowerShell ($buf = New-Object Byte[](3GB)).

Host Reaction: Physical host RAM hit 96% utilization. The Windows Host OS expanded its pagefile on the SSD (Committed memory spiked to 24.3 GB), demonstrating live virtual memory paging/swapping.

6. Post-Experiment Restoration
Following the experiment, the load scripts were stopped and both virtual machines were shut down to return memory allocations back to safe production values:

Ubuntu (lab01): Returned to 2048 MB (2 GB)

Windows 11 (lab02-win11): Returned to 4096 MB (4 GB)

Total Sane Allocation: 6.0 GB (Host stability fully restored).
