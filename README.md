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

**Host System:**
- OS: Debian 13 Trixie (Gnome)
- CPU: AMD Ryzen 9 9900X
- RAM: 64GB
- GPU: NVIDIA GeForce RTX 5070 Ti
- Virtualization: Virtual Machine Manager, QEMU/KVM

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
- Kali Linux toolset

## 📁 Repository Structure

    homelab/
    ├── setup/          # Lab configuration and setup guides
    ├── writeups/       # Security assessment writeups
    ├── scripts/        # Security automation scripts (in progress)
    └── README.md       # This file

## 🔍 Completed Exercises

### Exploitation & Vulnerability Assessment

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
- TCM Security BFCM CTF- Prompt Injecting LLM on TCM Website for entry to win free training

**In Progress:**
- CompTIA Security+ (exam May 2026)

**Future Goals:**
- Advanced penetration testing techniques
- Web application security testing
- Security automation with Python
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

**Last Updated:** April 2026

## 📫 Connect
- **LinkedIn:** [linkedin.com/in/gabriel-orta](https://linkedin.com/in/gabriel-orta)
- **GitHub:** [github.com/Scripted-G](https://github.com/Scripted-G)
