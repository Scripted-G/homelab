[README.md](https://github.com/user-attachments/files/33264860/README.md)
# 🖥️ Homelab

A hands-on environment for building practical skills across Windows administration, Active Directory, virtualization, Linux, networking, security testing, scripting, and local AI.

This repository documents the systems I build, configure, troubleshoot, and test
as I continue developing broader IT and cybersecurity skills.

---

## 🎯 Purpose

I use this homelab to gain hands-on experience with:

- Windows Server and Windows client administration
- Active Directory
- Virtualization with VMware Workstation Pro
- Linux system administration
- Virtual networking and segmentation
- Security testing in controlled environments
- Bash scripting and Python programming
- Local AI models
- Technical documentation, troubleshooting, and lab writeups

---

## 🧰 Host Environment

| Component | Current Setup |
|---|---|
| **Host OS** | Windows 11 Pro |
| **CPU** | AMD Ryzen 9 9900X |
| **RAM** | 64 GB DDR5 |
| **GPU** | Sapphire Pulse Radeon RX 9070 XT 16 GB |
| **Virtualization** | VMware Workstation Pro |
| **VM Organization** | Library folders: `SecLab` and `Dev` |

---

## 💾 Storage Layout

| Drive | Current Use |
|---|---|
| **500 GB NVMe** | Windows 11 host OS and normal system use |
| **2 TB NVMe** | Steam library and local AI models/data |
| **1 TB NVMe (D:)** | Homelab: VM disks (`D:\VM`) and ISO images (`D:\ISO`) |

---

## 🗂️ Current Lab Architecture

    Windows 11 Pro Host
    ├── VMware Workstation Pro
    │   ├── SecLab
    │   │   ├── Kali Linux
    │   │   ├── Metasploitable 2
    │   │   ├── Windows Server 2022
    │   │   └── Windows 11 Pro
    │   └── Dev
    │       └── Ubuntu 26.04 test VM
    │
    ├── Local AI
    │   └── LM Studio
    │
    └── Storage
        ├── 500 GB NVMe: Host OS
        ├── 2 TB NVMe: Steam + AI data
        ├── 1 TB NVMe: VMs + ISOs

---

## 🖥️ Virtual Machines

### SecLab

- **Kali Linux**: main security-testing VM
- **Metasploitable 2**: intentionally vulnerable target
- **Windows Server 2022**: provisioned for Windows Server and Active Directory work
- **Windows 11 Pro**: provisioned for Windows administration and domain-client work

### Dev

- **Ubuntu 26.04**: temporary validation and testing VM

---

## 🌐 Networking

### Current State

All VMs currently use VMware Workstation's default NAT networking.

Dedicated network segmentation has **not** yet been implemented in the current
VMware environment.

### Planned Work

The next networking phase will focus on building a more realistic lab design with
separate network segments for Windows/Active Directory and security testing.

---

## 🪟 Windows & Active Directory Lab

The Windows Server 2022 and Windows 11 Pro VMs are installed and updated, but the
Active Directory environment has not yet been built in the current VMware
environment.

### Planned Work

- Configure Windows Server 2022 as a domain controller
- Join the Windows 11 Pro client to the domain
- Build the supporting virtual network
- Practice users, groups, OUs, Group Policy, DNS, and domain administration
- Document the build as it progresses

---

## 🔐 Security Lab

The current security lab includes:

- **Kali Linux**
- **Metasploitable 2**

Both VMs are installed and usable. Metasploitable 2 is intentionally left in its
vulnerable state for controlled lab exercises.

Security work to date includes reconnaissance, service enumeration, API testing,
and exploitation of intentionally vulnerable systems. The writeups below were
completed on an earlier version of this lab that ran on Ubuntu with
QEMU/KVM/libvirt, before I moved the lab to a Windows host with VMware
Workstation Pro.

---

## 🤖 Local AI

I run local language models on the Windows host using **LM Studio**. This is a
newer area for me, and I'm using it to learn how local model hosting works.

---

## 📁 Repository Structure

    homelab/
    ├── setup/          # Environment setup and configuration documentation
    ├── writeups/       # Lab exercises and technical writeups
    ├── scripts/        # Automation and helper scripts
    └── README.md

---

## 📝 Selected Writeups

### Home Network Security Assessment

Authorized assessment of a personal home network using reconnaissance, service
enumeration, and device identification techniques.

[Read the writeup](writeups/home-network-assessment.md)

### Roku API Reconnaissance

Exploration of the Roku External Control Protocol using Nmap and `curl`, including
device discovery, API enumeration, and control testing.

[Read the writeup](writeups/roku-api-reconnaissance.md)

### vsftpd 2.3.4 Backdoor on Metasploitable 2

Controlled exploitation exercise against the intentionally vulnerable
Metasploitable 2 VM using Nmap and Metasploit.

[Read the writeup](writeups/vsftpd-exploit-writeup.md)

---

## 📚 Current Learning Areas

- Windows Server and Active Directory
- Networking and network segmentation
- Linux system administration
- VMware Workstation Pro
- Bash automation
- Python
- Security testing fundamentals
- Local AI (LM Studio)

---

## 🚧 Planned Work

- Build the Active Directory environment
- Build segmented homelab networking
- Expand automation and helper scripts
- Continue documenting security exercises and lab builds

---

## ⚖️ Responsible Use

Security testing documented in this repository is performed only on systems I own,
intentionally vulnerable lab targets, or systems for which I have explicit
authorization.

---

## 🔗 Connect

- [LinkedIn](https://linkedin.com/in/gabriel-orta)
- [GitHub](https://github.com/Scripted-G)
