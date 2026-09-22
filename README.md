# 🖥️ Homelab

A hands-on environment for building practical skills across Linux, virtualization,
networking, Windows administration, Active Directory, security testing, automation,
and local AI infrastructure.

This repository documents the systems I build, configure, troubleshoot, and test
as I continue developing broader IT and cybersecurity skills.

---

## 🎯 Purpose

I use this homelab to gain hands-on experience with:

- Linux system administration
- QEMU/KVM/libvirt virtualization
- Windows Server and Windows client administration
- Active Directory
- Virtual networking and segmentation
- Security testing in controlled environments
- Bash and Python automation
- Docker and local AI infrastructure
- Technical documentation and troubleshooting

---

## 🧰 Host Environment

| Component | Current Setup |
|---|---|
| **Host OS** | Ubuntu 26.04 LTS |
| **CPU** | AMD Ryzen 9 9900X |
| **RAM** | 32 GB DDR5 |
| **GPU** | Sapphire Pulse Radeon RX 9070 XT 16 GB |
| **Virtualization** | QEMU/KVM + libvirt |
| **VM Management** | virt-manager |

---

## 💾 Storage Layout

| Drive | Current Use |
|---|---|
| **500 GB NVMe** | Ubuntu host OS and normal system use |
| **2 TB NVMe** | Steam library and local AI workloads/data |
| **1 TB NVMe** | VM disks, snapshots, and frequently used ISO images |
| **Fourth NVMe** | Currently unassigned |

---

## 🗂️ Current Lab Architecture

    Ubuntu 26.04 LTS Host
    ├── QEMU/KVM + libvirt
    │   ├── Kali Linux
    │   ├── Metasploitable 2
    │   ├── Windows Server 2022
    │   ├── Windows 11 Pro
    │   ├── Ubuntu 26.04 test VM
    │   └── Jebetha project VM
    │
    ├── Local AI
    │   ├── Ollama
    │   ├── Open WebUI
    │   ├── Docker
    │   └── Radeon RX 9070 XT GPU acceleration
    │
    └── Storage
        ├── 500 GB NVMe — Host OS
        ├── 2 TB NVMe — Steam + AI data
        ├── 1 TB NVMe — VMs + ISOs
        └── Fourth NVMe — Unassigned

---

## 🖥️ Virtual Machines

### Core Learning Environment

- **Kali Linux** — main security-testing VM
- **Metasploitable 2** — intentionally vulnerable target
- **Windows Server 2022** — provisioned for Windows Server and future Active Directory work
- **Windows 11 Pro** — provisioned for Windows administration and future domain-client work

### Additional VMs

- **Ubuntu 26.04** — temporary validation and testing VM
- **Jebetha** — separate Kali-based VM used for an open-source project

---

## 🌐 Networking

### Current State

All VMs currently use the default libvirt NAT network.

Dedicated segmentation has **not** yet been implemented on the current Ubuntu host.

### Planned Work

The next networking phase will focus on building a more realistic lab design with
separate network segments for Windows/Active Directory and security testing.

---

## 🪟 Windows & Active Directory Lab

The Windows Server 2022 and Windows 11 Pro VMs are installed and working, but the
Active Directory environment has not yet been rebuilt on the current
Ubuntu/QEMU/KVM host.

### Planned Work

- Configure Windows Server 2022 as a domain controller
- Join the Windows 11 Pro client to the domain
- Build the supporting virtual network
- Practice users, groups, OUs, Group Policy, DNS, and domain administration
- Document the rebuild as it progresses

---

## 🔐 Security Lab

The current security lab includes:

- **Kali Linux**
- **Metasploitable 2**

Both VMs are installed and usable. Metasploitable 2 is intentionally left in its
vulnerable state for controlled lab exercises.

Current security work includes reconnaissance, service enumeration, API testing,
and exploitation of intentionally vulnerable systems.

---

## 🤖 Local AI Environment

The Ubuntu host also runs a local AI environment built around:

- **Ollama**
- **Open WebUI**
- **Docker**
- AI model/data storage on the 2 TB NVMe
- GPU-accelerated inference using the Radeon RX 9070 XT

This environment gives me hands-on experience with local model hosting, Linux
services, containers, storage layout, and GPU-backed inference.

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

[Read the writeup](writeups/home-network-assessment-sanitized.md)

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

- Linux system administration
- Networking and network segmentation
- Active Directory
- Bash automation
- Python
- QEMU/KVM/libvirt
- Docker
- Local AI infrastructure
- Security testing fundamentals

---

## 🚧 Planned Work

- Build segmented homelab networking
- Rebuild the Active Directory environment
- Expand automation and helper scripts
- Continue documenting security exercises
- Expand local AI infrastructure documentation

---

## ⚖️ Responsible Use

Security testing documented in this repository is performed only on systems I own,
intentionally vulnerable lab targets, or systems for which I have explicit
authorization.

---

## 🔗 Connect

- [LinkedIn](https://linkedin.com/in/gabriel-orta)
- [GitHub](https://github.com/Scripted-G)
