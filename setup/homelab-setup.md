# 🛠️ Homelab Setup

This document describes the current setup of my Ubuntu-based homelab environment.

The lab is used for practical learning across Linux administration, virtualization,
networking, Windows administration, Active Directory, security testing, automation,
and local AI infrastructure.

---

## 🧰 Host System

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

The host currently uses four NVMe drives:

| Drive | Current Use |
|---|---|
| **500 GB NVMe** | Ubuntu host OS and normal system use |
| **2 TB NVMe** | Steam library and local AI workloads/data |
| **1 TB NVMe** | VM disks, snapshots, and frequently used ISO images |
| **Fourth NVMe** | Currently unassigned |

The 1 TB virtualization drive is used to keep VM storage separate from the host OS.

---

## 🖥️ Virtual Machines

### Kali Linux

Primary security-testing VM.

**Current state**
- Installed and usable
- Updated after installation
- Connected to the default libvirt NAT network

**Purpose**
- Network reconnaissance
- Security tooling
- Controlled lab exercises
- Interaction with intentionally vulnerable targets

---

### Metasploitable 2

Intentionally vulnerable target VM used for controlled security exercises.

**Current state**
- Installed and usable
- Connected to the default libvirt NAT network
- Intentionally not updated in order to preserve the vulnerable services it is designed to expose

**Purpose**
- Vulnerability identification
- Service enumeration
- Controlled exploitation practice
- Post-exploitation learning in a lab environment

---

### Windows Server 2022

Provisioned for Windows Server administration and a planned Active Directory lab rebuild.

**Current state**
- Installed and usable
- Connected to the default libvirt NAT network
- Active Directory is not currently configured

**Planned role**
- Domain controller
- DNS
- Active Directory administration
- Group Policy practice
- Windows infrastructure learning

---

### Windows 11 Pro

Provisioned for Windows administration and future Active Directory client work.

**Current state**
- Installed and usable
- Connected to the default libvirt NAT network
- Not currently joined to a domain

**Planned role**
- Domain-joined client
- Group Policy testing
- Windows endpoint administration
- Active Directory client-side practice

---

### Ubuntu 26.04

Temporary testing and validation VM.

This VM is used when I need a clean Ubuntu environment for testing changes without
risking the host system.

One example was validating the Ubuntu 26.04 Snap-removal automation script before
using or publishing it more broadly.

---

### Jebetha

Separate Kali-based VM dedicated to an open-source project.

Keeping this VM separate from the main Kali lab environment allows project-specific
changes and dependencies to remain isolated from the general-purpose security VM.

---

## 🌐 Current Network Configuration

At present, all VMs use the default libvirt NAT network.

There is no dedicated segmentation between the Windows, security, and project VMs yet.

### Planned networking work

The next phase of the homelab will focus on creating a more realistic virtual network
design, including separation between:

- Windows / Active Directory systems
- security-testing systems
- intentionally vulnerable targets
- other project-specific workloads

The exact design will be documented after it is built and tested.

---

## 🪟 Active Directory Status

The previous version of this lab used a configured Active Directory environment under
Windows and VMware Workstation Pro.

That environment has not yet been rebuilt on the current Ubuntu/QEMU/KVM host.

The Windows Server 2022 and Windows 11 Pro VMs are already provisioned and will be used
for the rebuild.

Planned work includes:

- configure Windows Server 2022 as a domain controller
- configure DNS for the lab
- create users, groups, and organizational units
- join Windows 11 Pro to the domain
- implement and test Group Policy
- document the virtual network design
- practice both administration and security concepts in the completed environment

---

## 🔐 Security Lab

The current security lab consists primarily of Kali Linux and Metasploitable 2.

The environment is used for controlled exercises such as:

- host and service discovery
- service-version enumeration
- vulnerability research
- controlled exploitation of intentionally vulnerable services
- API interaction and testing
- post-exploitation learning
- documentation of findings and remediation concepts

Security testing is limited to systems I own, intentionally vulnerable targets, or
systems for which I have explicit authorization.

---

## 🤖 Local AI Environment

The Ubuntu host also runs a local AI environment.

### Current components

- **Ollama**
- **Open WebUI**
- **Docker**
- **Radeon RX 9070 XT** for GPU-accelerated local inference
- AI model and application data stored on the 2 TB NVMe

This environment is used to learn more about:

- local model hosting
- Linux service management
- containers
- persistent storage
- GPU-backed inference
- local AI application integration

---

## 📸 Snapshots and Recovery

VM snapshots are used before major changes or lab exercises where rollback may be useful.

This is especially helpful for:

- Windows configuration changes
- Active Directory testing
- security exercises
- software or service changes
- experiments that may alter VM state significantly

---

## 🔑 SSH Access to Metasploitable 2

Metasploitable 2 uses older SSH algorithms that modern clients may reject by default.

A one-time connection from Kali can use:

    ssh -oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedKeyTypes=+ssh-rsa msfadmin@[METASPLOITABLE-IP]

For repeated use, a host entry can be added to `~/.ssh/config` on Kali:

    Host metasploitable
        HostName [METASPLOITABLE-IP]
        User msfadmin
        HostKeyAlgorithms +ssh-rsa
        PubkeyAcceptedKeyTypes +ssh-rsa

Then connect with:

    ssh metasploitable

Metasploitable 2 uses the default account:

    Username: msfadmin
    Password: msfadmin

---

## ⚠️ Notes

- Metasploitable 2 is intentionally vulnerable and should not be treated like a normal maintained system.
- The current lab network is still using the default libvirt NAT network.
- Dedicated network segmentation is planned but not yet implemented.
- The Active Directory environment is planned but not yet rebuilt on the current host.
- Documentation in this repository will be updated as those parts of the lab are completed.

---

## 🔗 Resources

- [Kali Linux Documentation](https://www.kali.org/docs/)
- [Metasploitable 2](https://sourceforge.net/projects/metasploitable/)
- [Rapid7 Metasploitable 2 Guide](https://docs.rapid7.com/metasploit/metasploitable-2/)
- [Windows Server 2022 Evaluation](https://www.microsoft.com/evalcenter/download-windows-server-2022)
