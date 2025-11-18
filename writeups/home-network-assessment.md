# Home Network Security Assessment

## Overview
Conducted a comprehensive security assessment of my home network to identify connected devices, open ports, and potential security vulnerabilities. This exercise demonstrates network reconnaissance techniques and device identification methodologies used in professional security assessments.

## Objective
- Map all devices on the home network
- Identify open ports and running services
- Assess security posture of networked devices
- Practice reconnaissance and enumeration techniques

## Tools Used
- **Nmap** - Network scanning and service detection
- **curl** - HTTP/API interaction and testing
- **telnet** - Service connection testing
- **MAC Vendor Lookup** - Device manufacturer identification

## Network Information
- **Network Range:** 10.0.0.0/24
- **Gateway:** 10.0.0.1
- **Scan Host:** 10.0.0.19 (Pop!_OS workstation)
- **Total Devices Found:** 14 active hosts

## Methodology

### Phase 1: Network Discovery

**Initial network scan to identify live hosts:**
```bash
nmap 10.0.0.0/24
```

**Results:**
- 14 hosts discovered on the network
- Mixture of network infrastructure, IoT devices, and personal computers

### Phase 2: Service Enumeration

**Detailed service scan on devices with open ports:**
```bash
nmap -sV [target-ip]
```

**Comprehensive port scan (all 65,535 ports):**
```bash
nmap -sV -p- [target-ip]
```

### Phase 3: Device Identification

**MAC address lookup for unknown devices:**
- Used macvendors.com to identify device manufacturers
- Cross-referenced with known household devices

### Phase 4: Security Assessment

**Attempted API interaction and service enumeration:**
```bash
curl http://[target-ip]:[port]
telnet [target-ip] [port]
```

## Findings

### Device Inventory

#### 10.0.0.1 - Primary Router/Gateway
**Open Ports:**
- 53/tcp (DNS)
- 80/tcp (HTTP - Admin interface)
- 443/tcp (HTTPS - Admin interface)

**Assessment:** Standard router configuration. Web interface requires authentication.

---

#### 10.0.0.3 - Tuya Smart Device (Smart Lock)
**Open Ports:**
- 6668/tcp (Tuya proprietary protocol)

**MAC Address:** 38:A5:C9:7B:F3:13 (Tuya Smart Inc)

**Services Identified:**
- Custom IoT communication protocol
- Does not respond to standard commands
- Connects to Tuya cloud services

**Security Assessment:**
- ✅ Minimal attack surface (single proprietary port)
- ✅ Does not expose web interface
- ✅ No standard protocols exposed

---

#### 10.0.0.4 - Netgear WiFi Extender/Repeater
**Open Ports:**
- 53/tcp (DNS - dnsmasq 2.85)
- 80/tcp (HTTP - Requires authentication)
- 443/tcp (HTTPS - Requires authentication)

**MAC Address:** 6C:CD:D6:2D:93:2B (Netgear)

**Services Identified:**
- dnsmasq DNS server
- Web administration interface (password protected)

**Security Assessment:**
- ✅ Authentication required for web interface (401 Unauthorized)
- ✅ Legitimate network services only
- ✅ Proper access controls in place

---

#### 10.0.0.5 - Roku Streaming Device
**Open Ports:**
- 7000/tcp (RTSP - AirTunes rtspd 377.40.00)
- 8060/tcp (UPnP - Roku External Control Protocol)
- 40133/tcp (Unknown service)

**MAC Address:** 10:59:32:C7:D6:93 (Roku)

**Device Details:**
- Model: Roku 3920RW
- Friendly Name: "Roku FR"
- Roku Streaming Player Network Media

**Services Identified:**
- RTSP streaming service (AirPlay functionality)
- External Control Protocol API (remote control)
- Additional proprietary service

**Security Assessment:**
- ✅ **Limited Mode enabled** - Blocks external control commands
- ✅ ECP API returns: "ECP command not allowed in Limited mode"
- ✅ Minimal attack surface
- ✅ Properly secured with access restrictions

**API Testing:**
```bash
# Device information query (allowed)
curl http://10.0.0.5:8060
# Returns device XML information

# App list query (blocked)
curl http://10.0.0.5:8060/query/apps
# Returns: "ECP command not allowed in Limited mode"

# Remote control attempts (blocked)
curl -d '' http://10.0.0.5:8060/keypress/Home
# No response - command blocked
```

---

#### 10.0.0.8 - Unknown Device
**Open Ports:**
- 80/tcp (HTTP)
- 443/tcp (HTTPS)

**Assessment:** Network device with web interface. Further investigation required.

---

#### 10.0.0.19 - Pop!_OS Workstation (This Machine)
**Open Ports:** NONE

**Assessment:**
- ✅ All ports closed - excellent security posture
- ✅ Firewall properly configured
- ✅ No unnecessary services exposed
- ✅ Secure workstation configuration

---

#### Additional Devices (10.0.0.10, 12, 13, 14, 15, 16, 17, 24)
**Open Ports:** None detected

**Assessment:** Likely mobile devices (phones, tablets) and other consumer electronics with no services exposed. Good security posture.

## Security Analysis

### Overall Network Security Posture: GOOD

**Strengths:**
1. **Minimal Open Ports** - Most devices have no exposed services
2. **Authentication Required** - Network devices require login credentials
3. **IoT Security Controls** - Smart devices use proprietary protocols with limited attack surface
4. **Roku Limited Mode** - Prevents unauthorized remote control
5. **Workstation Security** - Personal computer properly locked down

**Observations:**
1. **Three-tier network infrastructure** - ISP modem + two WiFi repeaters for coverage
2. **Mixed device ecosystem** - Network infrastructure, IoT devices, streaming devices, personal computers
3. **Proper segmentation** - Devices only expose necessary services
4. **Access controls functioning** - Web interfaces require authentication

### Attack Surface Assessment

**Low Risk Devices:**
- Personal workstation (10.0.0.19) - All ports closed
- Mobile devices - No services exposed
- Roku (10.0.0.5) - Limited Mode prevents abuse

**Medium Risk Devices:**
- Router/Gateway (10.0.0.1) - Standard risk; requires strong password
- WiFi Extender (10.0.0.4) - Standard risk; requires strong password

**Minimal Risk IoT:**
- Smart Lock (10.0.0.3) - Proprietary protocol, minimal exposure

## Key Takeaways

### Technical Skills Demonstrated
1. **Network Reconnaissance** - Successfully mapped entire home network
2. **Service Enumeration** - Identified services and versions on open ports
3. **Device Fingerprinting** - Used MAC addresses to identify device manufacturers
4. **API Discovery** - Found and tested Roku ECP API
5. **Security Assessment** - Evaluated security controls and access restrictions
6. **Protocol Analysis** - Attempted various connection methods (HTTP, telnet, API calls)

### Security Lessons Learned
1. **Security settings work** - Limited Mode on Roku effectively blocked unauthorized access
2. **Minimal services = smaller attack surface** - Devices with fewer open ports are more secure
3. **Authentication matters** - Web interfaces protected by login prevent casual exploitation
4. **IoT can be secure** - Proprietary protocols and limited exposure reduce risk
5. **Proper workstation hardening** - Closed ports indicate good security practices

### Real-World Applications
This assessment demonstrates skills directly applicable to:
- **SOC Analyst roles** - Network monitoring and device inventory
- **Security Analyst positions** - Risk assessment and vulnerability identification
- **Penetration Testing** - Reconnaissance and enumeration phases
- **Network Security** - Understanding device security postures

## Remediation Recommendations

**Current State:** Network is well-secured with no critical vulnerabilities identified.

**Best Practices Observed:**
- ✅ Minimal services exposed
- ✅ Authentication on admin interfaces
- ✅ IoT devices properly configured
- ✅ Workstation firewall active

**Optional Enhancements:**
1. **Network Segmentation** - Consider VLAN separation for IoT devices
2. **Regular Updates** - Ensure all network devices have latest firmware
3. **Strong Passwords** - Verify router/repeater admin passwords are complex
4. **Monitor Unknown Devices** - Investigate 10.0.0.8 further to identify purpose

## Ethical Considerations

**Scope of Assessment:**
- ✅ All devices scanned are on personal home network
- ✅ Full authorization to test own devices
- ✅ No attempts to bypass security controls when blocked
- ✅ Assessment stopped at security boundaries

**Responsible Disclosure:**
- No vulnerabilities requiring disclosure were discovered
- All devices demonstrated appropriate security controls
- Roku Limited Mode functioned as designed

## Conclusion

This home network security assessment successfully identified all active devices, enumerated services, and evaluated security postures. The network demonstrates good security practices with minimal attack surface, proper authentication controls, and effective security features like Roku's Limited Mode.

**Skills Practiced:**
- Network scanning and reconnaissance
- Service enumeration and identification
- Device fingerprinting via MAC addresses
- API interaction and testing
- Security control evaluation
- Professional documentation

**Assessment Outcome:** Network is properly secured with no immediate vulnerabilities requiring remediation. All devices demonstrate appropriate security configurations for their intended purposes.

---

**Date:** November 18, 2025  
**Assessed By:** Gabriel  
**Network:** Home LAN (10.0.0.0/24)  
**Total Scan Time:** ~2 hours  
**Tools Used:** Nmap 7.80, curl, telnet, macvendors.com
