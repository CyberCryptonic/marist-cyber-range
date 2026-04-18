# Marist SOC Cyber Range — SOC Environment IP Addressing Scheme

## Overview
This document tracks all IP address assignments for the SOC / Detection Environment.  
Maintaining this file ensures consistent configuration, prevents IP conflicts, and supports scalability as additional SOC systems are deployed.

---

# 🌐 SOC / Detection Environment — IP Configuration

## Purpose

This document defines the IP addressing scheme for the SOC Environment.

It ensures:
- consistent system configuration
- no IP conflicts
- easier troubleshooting
- scalability as additional systems are added

---

## Related Setup Phases

- Used in: Phase 01 — SOC Environment Initialization
- Referenced by all future SOC deployment phases

---

## SOC Network
Subnet: `10.20.30.0/24`  
Gateway: `10.20.30.1`

---

## 🔹 Core SOC Infrastructure

| System Name                     | Hostname                      | IP Address     |
|--------------------------------|-------------------------------|----------------|
| Security Onion Platform        | Security-Onion                | 10.20.30.10    |
| Firewall & Segmentation Server | Firewall-Segmentation         | 10.20.30.20    |
| Linux Log Server               | Linux-Log-Server              | 10.20.30.30    |
| Core Network Router            | Core-Network-Router           | 10.20.30.40    |

---

## 🔹 Detection / Simulation Systems

| System Name                     | Hostname                        | IP Address     |
|--------------------------------|----------------------------------|----------------|
| Adversary Simulation Server    | Adversary-Simulation             | 10.20.30.50    |
| Cyber Range Orchestration      | Range-Orchestration              | 10.20.30.70    |

---

## 🔹 SOC Workstations

| System Name              | Hostname                | IP Address     |
|-------------------------|--------------------------|----------------|
| SOC Admin Workstation   | SOC-Admin-Workstation   | DHCP / Reserved |
| SOC Analyst Workstation | SOC-Analyst-Workstation | DHCP / Reserved |

---

# 📌 IP Addressing Strategy

- `.1` → Gateway / Firewall
- `.10–.40` → Core SOC infrastructure
- `.50–.70` → Simulation & traffic systems
- `.100–.200` → DHCP client range (workstations)
- `.200+` → Future expansion (additional tools, integrations, sensors)

---

# ⚠️ Rules & Best Practices

- Never assign duplicate IP addresses
- Always update this document before deploying new systems
- Maintain consistent hostname naming conventions
- SOC systems should use Target Environment DNS:
  - Primary DNS: `10.20.20.10`
  - Secondary DNS: `10.20.20.11`
- Security Onion is NOT domain joined:
  - Uses DNS for resolution only
- SOC Workstations ARE domain joined to:
  - `cyberrange.local`
- Ensure proper network segmentation between:
  - SOC Environment (10.20.30.0/24)
  - Target Environment (10.20.20.0/24)
- Monitoring interfaces (Security Onion) must connect to Target network for visibility

---

# 🔄 Change Management

- Any new SOC system must be assigned an IP before deployment
- Update this file immediately after adding:
  - New servers
  - Detection tools
  - Simulation systems
- Do not reuse IP addresses without verification

---

# 📍 Phase 01 Status

The following systems are fully deployed and validated:

- Security Onion → `10.20.30.10`
- SOC Admin Workstation → DHCP
- SOC Analyst Workstation → DHCP

Remaining systems will be deployed in future phases.

---
