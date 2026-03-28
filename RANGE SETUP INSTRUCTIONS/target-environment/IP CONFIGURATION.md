# Marist SOC Cyber Range — IP Addressing Scheme

## Overview
This document tracks all IP address assignments for the cyber range environment.  
Maintaining this file prevents IP conflicts, simplifies troubleshooting, and ensures consistency as the environment scales.

# Target Environment — IP Configuration

## Purpose

This document defines the IP addressing scheme for the Target Environment.

It ensures:
- consistent system configuration
- no IP conflicts
- easier troubleshooting
- scalability as additional systems are added

## Related Setup Phases

- Used in: Phase 01 — Networking
- Referenced by all system deployment phases

---

# 🌐 Network Segmentation

## Red Team Network
Subnet: `10.20.10.0/24`  
Gateway: `10.20.10.1`

> (To be populated)

---

## Target Network
Subnet: `10.20.20.0/24`  
Gateway: `10.20.20.1`

### 🔹 Core Infrastructure

| System Name              | Hostname                  | IP Address     |
|-------------------------|--------------------------|----------------|
| Domain Controller       | Primary-Domain-Server    | 10.20.20.10    |
| File Server             | File-Server              | 10.20.20.30    |

---

### 🔹 Windows 10 Workstations

| System Name              | Hostname         | IP Address     |
|-------------------------|------------------|----------------|
| Windows 10 User 01      | WIN10-User01     | 10.20.20.101   |
| Windows 10 User 02      | WIN10-User02     | 10.20.20.102   |
| Windows 10 User 03      | WIN10-User03     | 10.20.20.103   |

---

### 🔹 Windows 11 Workstations

| System Name              | Hostname         | IP Address     |
|-------------------------|------------------|----------------|
| Windows 11 User 01      | WIN11-User01     | 10.20.20.111   |
| Windows 11 User 02      | WIN11-User02     | 10.20.20.112   |
| Windows 11 User 03      | WIN11-User03     | 10.20.20.113   |

---

## SOC / Detection Network
Subnet: `10.20.30.0/24`  
Gateway: `10.20.30.1`

> (To be populated)

---

# 📌 IP Addressing Strategy

- `.1` → Gateway / Firewall
- `.10–.50` → Core servers (DC, File Server, future infrastructure)
- `.100–.109` → Windows 10 endpoints
- `.110–.119` → Windows 11 endpoints
- `.200+` → Future expansion (tools, SIEM agents, testing systems)

---

# ⚠️ Rules & Best Practices

- Never assign duplicate IP addresses
- Always update this document before deploying new machines
- Use consistent naming conventions for all hosts
- All domain-joined systems must use:
  - DNS: `10.20.20.10` (Domain Controller)
- Avoid reusing IPs unless confirmed unused across the environment

---

# 🚀 Future Additions

- Red Team machine IP assignments
- SOC/Detection tools (Security Onion, SIEM, log forwarders)
- Admin / management workstations
- Vulnerable application servers

---

# 🧠 Notes

This file should be continuously updated as the environment evolves.  
It serves as the single source of truth for network addressing within the cyber range.
