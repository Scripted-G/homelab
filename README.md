# Homelab
Hands-on cybersecurity practice environment for offensive security, 
penetration testing, and Active Directory research. This repository 
documents practical security skills built through controlled lab exercises.

## 🎯 Purpose
This homelab serves as a safe, isolated environment where I can:
- Practice penetration testing methodologies
- Exploit known vulnerabilities in a controlled setting
- Document security assessments and findings
- Develop security automation scripts
- Build hands-on experience with Active Directory attacks and defense

## 🛠️ Lab Environment
```
[Host: Windows 11 IoT LTSC]
                    [VMware Workstation Pro]
                              │
              ┌───────────────┴───────────────┐
              │                               │
       [Offensive Lab]                  [AD Lab]
       (NAT network)                    (Isolated network)
              │                               │
       ┌──────┴──────┐                ┌──────┴──────┐
       │             │                │             │
   Kali Linux  Metasploitable 2  Server 2022   Win 11 Pro
                                  (DC)         (Domain Client)
```

**Host System:**
- OS: Windows 11 IoT LTSC (hardened: telemetry disabled, no Microsoft account, OneDrive blocked via Group Policy)
- CPU: AMD Ryzen 9 9900X
- RAM: 64GB DDR5
- GPU: NVIDIA Asus TUF RTX 5070 Ti
- Virtualization: VMware Workstation Pro
- Lab VMs: UEFI + Secure Boot, TPM passthrough for Windows 11 clients, isolated virtual networks per lab segment

**Virtual Machines:**

*Offensive Lab (NAT network)*
- **Kali Linux** — Primary attack platform
- **Metasploitable 2** — Intentionally vulnerable target

*Active Directory Lab (Isolated network)*
- **Windows Server 2022** — Domain Controller
- **Windows 11 Pro** — Domain-joined client

**Key Tools Used:**
- Metasploit Framework
- Nmap
- Wireshark
- Netcat
- Burp Suite

## 📁 Repository Structure

    homelab/
    ├── setup/          # Lab configuration and setup guides
    ├── writeups/       # Security assessment writeups
    ├── scripts/        # Security automation scripts (in progress)
    └── README.md       # This file

## 🔍 Completed Exercises

###  Reconnaissance & Exploitation

1. **vsftpd 2.3.4 Backdoor Exploitation**
   - Exploited known backdoor vulnerability in vsftpd on Metasploitable 2
   - Used Metasploit Framework for exploitation
   - Gained remote shell access with root privileges
   - [Full writeup →](writeups/vsftpd-exploit-writeup.md)

2. **Home Network Security Assessment**
   - Comprehensive scan of home network infrastructure
   - Identified active hosts, open services, and security posture
   - Documented findings and recommendations
   - [Full writeup →](writeups/home-network-assessment-sanitized.md)

3. **Roku API Reconnaissance**
   - Discovered and enumerated Roku ECP API endpoints
   - Tested device security controls
   - Documented attack surface and remediation
   - [Full writeup →](writeups/roku-api-reconnaissance.md)

## 📚 Setup Documentation
- [Homelab Setup Guide →](setup/homelab-setup.md)

## 🎓 Learning Path

**Completed:**
- TCM Security 2025 Black Friday CTF — Successfully completed the prompt injection challenge to earn a free training entry. Writeup forthcoming as part of a planned AI/LLM security series including Lakera Gandalf and similar exercises.

**In Progress:**
- CompTIA CySA+ (planned summer 2026)
- BloodHound and AD attack chains in the lab
- Burp Suite Professional workflows on intentionally vulnerable web apps (DVWA, Juice Shop)
- Building offensive tooling in C and Go
- OSCP preparation

## 🔐 Skills Demonstrated
- **Reconnaissance & Enumeration** — Network mapping, service and version 
  identification, IoT API discovery
- **Exploitation** — Leveraging known vulnerabilities using industry-standard tools
- **Active Directory** — Domain controller setup, domain joining, 
  environment configuration
- **Documentation** — Clear, professional security writeups with methodology, 
  findings, and remediation
- **Lab Management** — Building and maintaining isolated testing environments

## ⚠️ Ethical Use Disclaimer
All exercises in this repository are conducted in a controlled, isolated lab 
environment on systems I own or have explicit permission to test. This work 
is for educational purposes only.

**I do not engage in or condone:**
- Unauthorized access to computer systems
- Malicious hacking or illegal activities
- Testing on systems without explicit permission

## 📝 How to Use This Repository

**For Recruiters/Employers:**
- Browse the [writeups/](writeups/) folder for security assessment documentation
- Review [setup/](setup/) to understand lab configuration
- Check commit history to see ongoing development

**For Fellow Learners:**
- Use the setup guide as reference for your own lab
- Writeups include step-by-step methodology
- Feel free to reach out with questions

## 🔄 Updates
This repository is actively maintained and updated with new exercises, 
writeups, and scripts.

## 📫 Connect
- **LinkedIn:** [linkedin.com/in/gabriel-orta](https://linkedin.com/in/gabriel-orta)
- **GitHub:** [github.com/Scripted-G](https://github.com/Scripted-G)
