# Cybersecurity Homelab Setup

## Overview
This document outlines the setup of my cybersecurity homelab environment 
using KVM/QEMU on Fedora 44. The lab provides a safe, isolated environment 
for practicing penetration testing, Active Directory administration, and 
security operations.

## Host System

| Component | Details |
|-----------|---------|
| OS | Fedora 44 (Gnome) |
| Virtualization | Virtual Machine Manager & QEMU/KVM |
| CPU | AMD Ryzen 9 9900X |
| RAM | 64 GB DDR5 |
| GPU | NVIDIA Asus TUF RTX 5070Ti |

## Network Configuration

Two separate virtual networks isolate lab environments:

**NAT Network**
- Used by Kali Linux and Metasploitable 2
- Provides internet access for updates and tool downloads
- Isolates offensive lab traffic from the AD lab

**Internal-Lab (LAN Segment)**
- Used by WS22-DC and Win11-Pro
- Win11-Pro accesses internet through WS22-DC
- Mirrors enterprise network design where clients route through the domain controller
- Isolates client traffic from direct internet access

## Virtual Machines

### Kali Linux
Primary penetration testing platform.

| Resource | Allocation |
|----------|------------|
| RAM | 4 GB |
| CPUs | 4 |
| Disk | 80.1 GB |
| Network | NAT |

### Metasploitable 2
Intentionally vulnerable target system for exploitation practice.

| Resource | Allocation |
|----------|------------|
| RAM | 2 GB |
| CPUs | 2 |
| Disk | 8 GB |
| Network | NAT |
| OS | Ubuntu 8.04 (intentionally outdated) |

### WS22-DC (Windows Server 2022 Domain Controller)
Active Directory domain controller and server administration practice.

| Resource | Allocation |
|----------|------------|
| RAM | 4 GB |
| CPUs | 4 |
| Disk | 60 GB (NVMe) |
| Network Adapter 1 | NAT |
| Network Adapter 2 | LAN Segment — Internal-Lab |

### Win11-Pro (Windows 11 Pro)
Domain-joined client for endpoint testing and AD practice.

| Resource | Allocation |
|----------|------------|
| RAM | 4 GB |
| CPUs | 4 |
| Disk | 64 GB (NVMe) |
| Network | LAN Segment — Internal-Lab |

## Setup Instructions

### Kali Linux
1. Download the official Kali Linux ISO from kali.org
2. Open Virtual Machine Manager and create a new VM
3. Select the downloaded ISO as installation media
4. Allocate resources (4 GB RAM, 4 CPUs, 80 GB disk)
5. Set network adapter to NAT
6. Complete the standard Kali installation

### Metasploitable 2
Metasploitable 2 is distributed as a VMware image and can be imported directly.

1. Download Metasploitable 2 from Rapid7
2. Extract the archive
3. Open Virtual Machine Manager
4. Select "Create New Virtual Machine" and browse to the extracted .vmx file
5. Set network adapter to NAT
6. Allocate resources (2 GB RAM, 2 CPUs)

Default credentials: msfadmin / msfadmin

### WS22-DC (Windows Server 2022)
1. Download the Windows Server 2022 ISO from Microsoft Evaluation Center
2. Open Virtual Machine Manager and create a new VM
3. Select the downloaded ISO as installation media
4. Allocate resources (4 GB RAM, 4 CPUs, 60 GB disk)
5. Add two network adapters — NAT and LAN Segment (Internal-Lab)
6. Complete the Windows Server installation
7. Configure as Active Directory Domain Controller

### Win11-Pro (Windows 11 Pro)
1. Download the Windows 11 ISO from Microsoft
2. Open Virtual Machine Manager and create a new VM
3. Select the downloaded ISO as installation media
4. Allocate resources (4 GB RAM, 4 CPUs, 64 GB disk)
5. Set network adapter to LAN Segment (Internal-Lab)
6. Enable TPM 2.0 in VM settings (required for Windows 11)
7. Complete the Windows 11 installation
8. Join the domain hosted on WS22-DC

## SSH Access to Metasploitable 2
Metasploitable 2 uses older SSH algorithms that modern clients reject by default.

One-time connection from Kali:

    ssh -oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedKeyTypes=+ssh-rsa msfadmin@[METASPLOITABLE-IP]

Permanent configuration — add to ~/.ssh/config on Kali:

    Host metasploitable
        HostName [METASPLOITABLE-IP]
        User msfadmin
        HostKeyAlgorithms +ssh-rsa
        PubkeyAcceptedKeyTypes +ssh-rsa

Then connect with:

    ssh metasploitable
    Password: msfadmin

## Security Considerations
- **Isolation**: Offensive lab (Kali + Metasploitable) on NAT. AD lab on 
  Internal-Lab LAN Segment — Win11-Pro routes internet traffic through 
  WS22-DC, mirroring enterprise network design.
- **No Updates**: Metasploitable 2 is intentionally NOT updated to preserve 
  vulnerabilities
- **Snapshots**: Take VM snapshots before major changes for easy recovery
- **Legal**: Only test on systems you own or have explicit permission to test

## Resources
- Metasploitable 2: https://sourceforge.net/projects/metasploitable/
- Kali Linux Documentation: https://www.kali.org/docs/
- Rapid7 Metasploitable Guide: https://docs.rapid7.com/metasploit/metasploitable-2/
- Windows Server Evaluation: https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022

---
