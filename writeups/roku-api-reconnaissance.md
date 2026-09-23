# Roku API Reconnaissance and Interaction

## Overview

This writeup documents an authorized assessment of a personally owned Roku streaming
device using network discovery, service enumeration, and interaction with Roku's
External Control Protocol (ECP).

The exercise focused on understanding what the device exposed to the local network,
how the API behaved during testing, and what security implications follow from
local-network access.

---

## Objective

- Identify the Roku device on the local network
- Enumerate exposed services
- Interact with the Roku ECP API
- Test application and navigation control
- Document the device's local-network attack surface
- Compare the observed behavior with Roku's documented ECP controls

---

## Environment

- **Environment:** Personal home network
- **Authorization:** Full authorization; personally owned device
- **Target:** Roku 3920RW
- **Primary tools:** Kali Linux, Nmap, `curl`
- **API:** Roku External Control Protocol (ECP)

> **Privacy note:** IP addresses in this document are represented with representative private RFC1918 addresses. The methodology and observed behavior are based on the original exercise.

---

## Tools Used

- **Nmap** — host discovery and service enumeration
- **curl** — HTTP requests and API interaction

---

## Methodology

### 1. Device Discovery

An initial network scan was used to identify the Roku device:

```bash
nmap 192.168.1.0/24
```

The device was identified through its network presence and exposed services.

---

### 2. ECP Service Testing

The Roku ECP interface was tested on TCP port 8060:

```bash
curl http://192.168.1.50:8060
```

The device returned XML information describing the Roku platform and available
services.

---

### 3. Application Enumeration

Installed applications were queried with:

```bash
curl http://192.168.1.50:8060/query/apps
```

The device returned the installed application list, confirming that ECP queries were
available from the local network during the assessment.

Sample applications included:

- Netflix
- YouTube
- Prime Video
- Hulu

---

### 4. Active Application Query

The currently active application was queried with:

```bash
curl http://192.168.1.50:8060/query/active-app
```

Example response:

```xml
<active-app>
    <app id="562859" type="home">Home</app>
</active-app>
```

This showed that the device was on the Roku home screen at the time of the query.

---

### 5. Remote-Control Testing

Application launch and navigation commands were tested through ECP.

To launch YouTube:

```bash
curl -d '' http://192.168.1.50:8060/launch/837
```

The active application was queried again to verify the result:

```bash
curl http://192.168.1.50:8060/query/active-app
```

The response showed YouTube as the active application.

A navigation command was also tested:

```bash
curl -d '' http://192.168.1.50:8060/keypress/Home
```

The device returned to the Roku home screen.

---

## Observed ECP Functionality

### Device Information

Examples of device-query endpoints included:

```text
GET /query/device-info
GET /query/apps
GET /query/active-app
```

### Application Control

Example:

```text
POST /launch/[APP_ID]
```

### Navigation Control

Examples:

```text
POST /keypress/Home
POST /keypress/Select
POST /keypress/Up
POST /keypress/Down
POST /keypress/Left
POST /keypress/Right
POST /keypress/Back
POST /keypress/Play
```

---

## Security Observations

During the assessment, the Roku device accepted ECP queries and local control commands
from another system on the same network.

Observed behavior included:

- device information could be queried
- installed applications could be enumerated
- the active application could be identified
- applications could be launched remotely
- navigation commands could be sent remotely

This behavior reflects intended ECP functionality, but it also demonstrates that
local-network access can provide meaningful control over the device when the relevant
control setting permits it.

The most important security boundary in this scenario was therefore the local network
itself and the Roku device's local-control configuration.

---

## Roku Control Settings and Current Behavior

Roku's current documentation describes three levels for **Control by mobile apps**:
**Limited**, **Enabled**, and **Permissive**.

Roku also documents that, beginning with Roku OS 14.1, several ECP commands — including
`keypress`, `keydown`, and `keyup` — require **Control by mobile apps** to be set to
**Enabled**.

That is relevant to this exercise because the Roku tested here accepted navigation and
application-control commands from the local network. The behavior observed during the
exercise therefore reflects a device configuration that permitted those ECP functions.

---

## Risk Context

The ECP interface was reachable from the local network during this exercise.

Another device with access to the same trusted network could potentially interact with
the Roku in similar ways when the Roku's control settings allow those commands.

The practical impact demonstrated in this exercise was limited to:

- local device discovery
- application enumeration
- active-application queries
- application launch
- navigation control

This exercise did not demonstrate remote internet exploitation, circumvention of Roku's local-control restrictions, or compromise of the underlying Roku operating system.

---

## Mitigation and Hardening

Potential ways to reduce unnecessary local-control exposure include:

- review the Roku's **Control by mobile apps** setting
- use Limited mode when broader local-control features are not required
- avoid exposing device-control services beyond the local network
- use network segmentation to separate IoT devices from general-purpose systems
- keep the Roku device and supporting network infrastructure updated
- periodically review which devices are able to communicate across the LAN

---

## Key Lessons

This exercise reinforced several concepts:

- IoT devices may expose useful local APIs even when they are not internet-facing
- API discovery can reveal meaningful device functionality
- local-network access should not automatically be treated as fully trusted
- intended functionality can still create security-relevant exposure
- device security behavior can change across software versions
- network segmentation can reduce the impact of compromised or untrusted devices
- observations from testing should be separated from claims based on external research

---

## Responsible Use

This exercise was performed only on a personally owned Roku device on a private
network under my control.

No testing was performed against systems or devices without authorization.

---

## Assessment Information

- **Date:** November 2025
- **Environment:** Personal home network
- **Device:** Roku 3920RW

---

## References

- [Roku Developer Documentation — External Control Protocol (ECP)](https://developer.roku.com/dev/docs/external-control-api)
- [Roku Support — Control by mobile apps](https://support.roku.com/en-gb/article/install-the-mobile-app)
- [Roku OS security update history](https://support.roku.com/en-us/article/roku-os-security-updates)
- [Roku Developer Forum — Roku OS 14.1 control-setting discussion](https://forum.developer.roku.com/t/tvinput-dtv-deep-linking-not-working/11262)
