# Ticket 1 — VM build document

## 1. What was asked
> "Hi, we have someone starting on Monday and he needs a test computer set up. Nothing special, just so he can try things without breaking anything. Can you write down how to do it so I can do the next one myself? Thanks" — Aigerim T. (Office Manager)

## 2. What was actually needed
* **Gaps in request:** The requester did not specify VM hardware specs (RAM, CPU, disk size), OS distributions (Linux vs Windows), hypervisor selection, network access requirements, or inter-guest communication needs.
* **Flawed assumptions:** The requester assumed an office manager without hypervisor experience could deploy a VM using a simple brief instruction. In practice, building a functional test environment requires hypervisor configuration, network setup, and clear step-by-step guidance explaining *why* specific options are chosen.
* **Assumptions made:**
  * Created two guest VMs: Linux (Ubuntu) and Windows 10/11 to cover full dev testing requirements.
  * Used NAT network adapter so guests share host's IP/MAC, bypassing Innotech teaching network MAC filtering.
  * Allocated resources dynamically based on the host system's real capacity to ensure host stability.

## 3. What I did
1. Audited host machine resources (Host: 16 GB RAM, 512 GB SSD).
2. Calculated guest allocations:
   * **Linux Guest:** 2 vCPU, 2048 MB RAM, 20 GB Dynamically Allocated Disk.
   * **Windows Guest:** 2 vCPU, 4096 MB RAM, 40 GB Dynamically Allocated Disk.
3. Configured VirtualBox with NAT networking to avoid network MAC blocking.
4. Installed operating systems on both guests with basic developer tools.
5. Tested internet connectivity and created snapshots for rollback.

### Non-default settings & justification:
* **Network Adapter: NAT (instead of Bridged)** — Innotech network filters by host MAC address; Bridged adapter assigns a new MAC which gets blocked. NAT routes through host MAC.
* **Disk Type: Dynamically Allocated** — Saves physical host disk space while allowing guest expansion if needed.

## 4. Evidence
* `evidence/01-new-vm-wizard.png`: Proves initial VM creation parameters and resource allocation.
* `evidence/02-disk-settings.png`: Proves dynamic disk allocation settings.
* `evidence/03-network-adapter.png`: Proves NAT network mode selection.
* `evidence/04-guest-uname.txt`: Terminal output (`uname -a`) proving Linux guest OS is running.
* `evidence/05-ping-between-guests.txt`: Output of `ping` proving external internet reachability.
* `evidence/06-snapshot-list.png`: Screenshot showing base system snapshot created for rollback.

## 5. What I would do differently
In the future, I would set up a Host-Only adapter as a second interface or configure a NAT Network subnet so that the Windows and Linux guest VMs can directly communicate with each other isolated from the external network, rather than relying solely on single NAT adapters.
