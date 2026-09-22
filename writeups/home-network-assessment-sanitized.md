# Home Network Security Assessment

## Overview

This writeup documents an authorized assessment of a personal home network using
basic reconnaissance, service enumeration, and device-identification techniques.

The goal was to identify active hosts, review exposed services, and document areas
that may warrant additional hardening or segmentation.

---

## Objective

- Identify active devices on the local network
- Enumerate open ports and running services
- Identify device types and manufacturers where possible
- Review the exposed attack surface of selected devices
- Document practical remediation ideas
- Practice network reconnaissance and technical documentation

---

## Environment

- **Environment:** Personal home network
- **Authorization:** Full authorization; all tested systems were personally owned or under my control
- **Primary tools:** Kali Linux, Nmap, `curl`, Telnet, MAC vendor lookup
- **Network type:** Standard residential network with mixed infrastructure, endpoint, and IoT devices

> **Privacy note:** IP addresses in this document are represented with RFC1918 example
> addresses. The methodology and observations are based on the original assessment.

---

## Tools Used

- **Nmap** — host discovery, port scanning, and service/version detection
- **curl** — HTTP and API interaction
- **Telnet** — basic service connectivity testing
- **MAC vendor lookup** — manufacturer identification

---

## Methodology

### 1. Host Discovery

Initial discovery scan:

```bash
nmap [NETWORK_RANGE]
```

**Result:** 14 active hosts were identified.

The discovered devices included network infrastructure, personal computers,
streaming devices, and IoT equipment.

---

### 2. Service Enumeration

Selected hosts were scanned for exposed services:

```bash
nmap -sV [TARGET_IP]
```

A full TCP port scan was also used where deeper enumeration was useful:

```bash
nmap -sV -p- [TARGET_IP]
```

---

### 3. Device Identification

Unknown devices were compared against MAC vendor information and known household
equipment to determine likely device type and manufacturer.

---

### 4. Service and API Testing

Where appropriate, exposed services were queried directly:

```bash
curl http://[TARGET_IP]:[PORT]
```

```bash
telnet [TARGET_IP] [PORT]
```

Testing remained limited to the local network and personally owned devices.

---

## Findings

### Primary Router / Gateway

**Observed TCP services**
- 53 — DNS
- 80 — HTTP management interface
- 443 — HTTPS management interface

The device exposed expected network-management services. Administrative interfaces
required authentication.

---

### Tuya Smart Device

**Observed TCP service**
- 6668 — Tuya proprietary protocol

The device did not expose a conventional web administration interface during the
assessment.

This reduced the number of directly exposed standard services, although the
proprietary service still represents part of the device's network attack surface.

---

### Netgear Wi-Fi Extender / Repeater

**Observed TCP services**
- 53 — DNS / dnsmasq
- 80 — HTTP management interface
- 443 — HTTPS management interface

The web interfaces required authentication.

The exposed services were consistent with the device's expected network-management
role.

---

### Roku Streaming Device

**Observed services included**
- 7000/tcp — streaming-related service
- 8060/tcp — Roku External Control Protocol (ECP)
- an additional proprietary service on a high TCP port

The Roku ECP interface was reachable from the local network.

During the dedicated Roku API exercise, the device accepted ECP queries and control
commands, including application enumeration and remote-control actions. This behavior
is documented separately in:

[Roku API Reconnaissance](roku-api-reconnaissance.md)

The key security consideration is that ECP control depends heavily on local-network
access and the Roku device's control settings.

---

### Unidentified Network Device

**Observed TCP services**
- 80 — HTTP
- 443 — HTTPS

The device exposed a web interface but was not conclusively identified during the
assessment.

Further investigation would be appropriate before drawing conclusions about its role
or security posture.

---

### Scanning Workstation

No listening TCP ports were identified by the scan performed during this assessment.

This indicates that the workstation was not exposing obvious TCP services at that
time. It should not be interpreted as proof that the system is fully secure.

---

### Additional Devices

Several additional devices did not expose TCP services during the scan.

These appeared to include mobile devices and consumer electronics.

Again, absence of detected listening ports reduces visible attack surface but does
not by itself establish overall device security.

---

## Security Observations

Several positive characteristics were observed:

- Many devices exposed few or no TCP services
- Administrative web interfaces required authentication
- The workstation did not expose obvious listening TCP services
- Network infrastructure exposed services consistent with its expected role

The assessment also identified areas worth improving:

- IoT and general-purpose systems shared the same residential network
- Device segmentation had not been implemented
- One device remained unidentified
- Local-network APIs such as Roku ECP demonstrated why trusted LAN access still matters
- Internet-facing exposure and router configuration should continue to be reviewed separately

---

## Attack Surface Summary

### Lower visible TCP exposure during this assessment

- Scanning workstation
- Several mobile/consumer devices

### Devices with identifiable exposed services

- Router / gateway
- Wi-Fi extender
- Tuya smart device
- Roku streaming device
- Unidentified web-enabled device

The presence of an open service is not automatically a vulnerability. Each service
needs to be evaluated in the context of authentication, configuration, software
version, network placement, and intended functionality.

---

## Recommendations

### Network Segmentation

Consider separating IoT devices from general-purpose computers using VLANs or another
segmented network design where supported by the network infrastructure.

### Firmware and Software Maintenance

Keep supported routers, extenders, streaming devices, and IoT equipment current with
vendor security updates.

### Administrative Access

Continue using strong credentials for router and network-device management interfaces.

### Unknown Devices

Identify and document devices that cannot immediately be accounted for.

### Local API Exposure

Review whether local-control features are needed on devices that expose APIs or remote
control functionality to the LAN.

### Ongoing Monitoring

Repeat discovery and service-enumeration checks periodically to identify unexpected
changes.

---

## Key Lessons

This exercise reinforced several practical concepts:

- Host discovery is only the beginning of a network assessment
- Service enumeration provides more useful context than host discovery alone
- Open ports must be interpreted in relation to device purpose and configuration
- IoT devices can expose meaningful local-network interfaces even when they are not
  internet-facing
- A lack of exposed services does not prove that a device is secure
- Network segmentation can reduce the impact of compromised or untrusted devices
- Clear documentation is important when distinguishing observations from conclusions

---

## Responsible Use

This assessment was conducted only on a personal network and devices under my control.

No testing was performed against systems without authorization.

---

## Assessment Information

- **Date:** November 2025
- **Environment:** Personal home network
- **Active hosts identified:** 14
