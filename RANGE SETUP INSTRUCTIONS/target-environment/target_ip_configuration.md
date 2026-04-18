# Marist SOC Cyber Range — IP Addressing Scheme

## Overview
This document tracks all IP address assignments for the cyber range environment.  
Maintaining this file prevents IP conflicts, simplifies troubleshooting, and ensures consistency as the environment scales.

# 🌐 Target Environment — IP Configuration

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

## Target Network
Subnet: `10.20.20.0/24`  
Gateway: `10.20.20.1`

### 🔹 Core Infrastructure

| System Name              | Hostname                  | IP Address     |
|-------------------------|--------------------------|----------------|
| Primary Domain Server   | Primary-Domain-Server    | 10.20.20.10    |
| Backup Domain Server    | Backup-Domain-Server     | 10.20.20.11    |
| Internal Web Server     | Internal-Web-Server      | 10.20.20.12    |
| Windows Log Server      | Windows-Log-Server       | 10.20.20.13    |
| Vulnerable Server       | Vuln-Training-Server     | 10.20.20.14    |
|Network Traffic Generator|Network-Traffic-Generator | 10.20.20.15    |
| File Server             | File-Server              | 10.20.20.30    |

---

### 🔹 Windows 10 Workstations (DHCP)

| System Name              | Hostname         | IP Address     |
|-------------------------|------------------|----------------|
| Windows 10 User 01      | WIN10-User01     | DHCP           |
| Windows 10 User 02      | WIN10-User02     | DHCP           |
| Windows 10 User 03      | WIN10-User03     | DHCP           |

---

### 🔹 Windows 11 Workstations (DHCP)

| System Name              | Hostname         | IP Address     |
|-------------------------|------------------|----------------|
| Windows 11 User 01      | WIN11-User01     | DHCP           |
| Windows 11 User 02      | WIN11-User02     | DHCP           |
| Windows 11 User 03      | WIN11-User03     | DHCP           |

---

### 🔹 Administrative & Analyst Systems

| System Name              | Hostname                     | IP Address     |
|-------------------------|------------------------------|----------------|
| IT Admin Workstation    | IT-Admin-Workstation         | 10.20.20.127   |
| Incident Response WS    | IR-Workstation               | 10.20.20.110   |
| Blue Team Analysis      | Blue-Team-Analysis           | 10.20.20.114   |

---

# 📌 IP Addressing Strategy

- `.1` → Gateway / Firewall
- `.10–.50` → Core servers (DC, File Server, infrastructure)
- `.100–.200` → DHCP client range
- Reserved IPs within DHCP range may be used for critical workstations (admin / analyst systems)
- `.200+` → Future expansion (tools, SIEM agents, testing systems)

---

# ⚠️ Rules & Best Practices

- Never assign duplicate IP addresses
- Always update this document before deploying new machines
- Use consistent naming conventions for all hosts
- All domain-joined systems must use:
  - DNS: `10.20.20.10` (Primary Domain Controller)
  - Secondary DNS: `10.20.20.11` (Backup Domain Controller)
- DHCP is managed externally (not on domain controllers)
- Avoid reusing IPs unless confirmed unused across the environment

---
