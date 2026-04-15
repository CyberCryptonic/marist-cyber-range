## Status 

✅ COMPLETE

# Marist SOC Cyber Range
# Lab Build Guide — Phase 01: Security Onion and SOC Workstation Deployment

---

# Phase Overview

Phase 01 focused on establishing the first fully working components of the SOC / Detection Environment.

This phase documents the systems that were completed and validated during this stage of the build:

- Security-Onion
- SOC-Admin-Workstation
- SOC-Analyst-Workstation

The purpose of this phase was to build the initial defensive monitoring platform and create dedicated analyst endpoints so the SOC environment could begin operating as a separate defensive space from the Target Environment.

> **Important scope note:** This guide documents only the systems that were actually completed during Phase 01. Other SOC environment systems shown in the full SOC topology are reserved for later phases.

---

# Phase 01 Objectives

The goal of this phase was to:

- Deploy a dedicated Security Onion monitoring platform in the SOC environment
- Place Security Onion on the SOC management subnet
- Attach a second interface for Target Environment monitoring visibility
- Configure Security Onion with a static IP and internal DNS resolution
- Build a dedicated SOC administrator workstation
- Build a dedicated SOC analyst workstation
- Join both SOC workstations to the domain
- Create SOC-specific Active Directory users, groups, and OUs
- Restrict SOC workstation access so regular domain users cannot sign in
- Access the Security Onion web interface from SOC workstations
- Resolve time synchronization issues that interfered with dashboard authentication

---

# Final Outcome

By the end of this phase, the environment included:

- A working **Security-Onion** VM deployed from the Security Onion 2.4 ISO
- A dedicated **SOC-Admin-Workstation**
- A dedicated **SOC-Analyst-Workstation**
- Both SOC workstations joined to `cyberrange.local`
- SOC-specific Active Directory users and security groups
- SOC-specific organizational units for users and workstations
- Group Policy-based access restrictions on the SOC workstations
- Working access to the Security Onion web interface from the SOC workstations
- Valid Security Onion web dashboard accounts for SOC users
- Corrected time alignment between the Security Onion VM and the Windows SOC workstations so web login would function properly

---

# Important Design Notes

## 1. Security Onion Version Selection

Security Onion 3.0 was not used due to instability during deployment.

The final working build used:

```text
securityonion-2.4 ISO
```

This guide documents only the final successful build path.

---

## 2. Security Onion Is Not Domain Joined

Security Onion was configured with:

```text
cyberrange.local
```

as its DNS search domain.

This does NOT mean it is joined to Active Directory.

- Uses AD DNS for name resolution
- Not domain joined
- SOC workstations ARE domain joined
- Dashboard users are created inside Security Onion

---

## 3. Network Design

Two NICs were used:

```text
Management NIC → vmbr3 (SOC network)
Monitoring NIC → vmbr2 (Target network visibility)
```

---

## 4. Time Synchronization Requirement

All systems in the cyber range MUST:

- Use the same timezone (Eastern Time - UTC -0400)
- Synchronize time from the domain controllers
- Maintain time alignment within a few seconds

Failure to maintain consistent time will result in:

- Authentication failures
- Security Onion dashboard login issues
- Incorrect log correlation

---

# 1. Build and Prepare the Security Onion VM

## 1.1 Download ISO

Download:

```text
securityonion-2.4.211-20260407.iso
```

---

## 1.2 Upload ISO to Proxmox

- Upload ISO to Proxmox storage
- Verify availability

---

## 1.3 Create VM

- Name: Security-Onion
- Attach ISO

---

## 1.4 Hardware Configuration

- RAM: 24GB
- CPU: 8 cores
- BIOS: OVMF (UEFI)
- Machine: q35
- Disk: 330GB
- SCSI: VirtIO

---

## 1.5 Network Configuration

- net0 → vmbr3 (Management)
- net1 → vmbr2 (Monitoring)

---

# 2. Install Security Onion

## 2.1 Boot ISO

Boot VM from ISO and begin install.

---

## 2.2 Configure Network

```text
IP: 10.20.30.10
Subnet: 255.255.255.0
Gateway: 10.20.30.1
DNS1: 10.20.20.10
DNS2: 10.20.20.11
Domain: cyberrange.local
```

---

## 2.3 Verify Interfaces

- ens18 → Management
- ens19 → Monitoring

---

# 3. Access Dashboard

```text
https://10.20.30.10
```

Access ONLY from SOC machines.

---

# 4. Build SOC Workstations

## 4.1 SOC Admin Workstation

- Windows 11
- Name: SOC-Admin-Workstation

## 4.2 SOC Analyst Workstation

- Windows 10/11
- Name: SOC-Analyst-Workstation

---

## 4.3 DNS Settings

```text
10.20.20.10
10.20.20.11
```

---

# 5. Join to Domain

- Domain: cyberrange.local
- Reboot after join
- Verify login works

---

# 6. Active Directory Setup

## 6.1 OUs

- SOC-WORKSTATIONS
- SOC-DEPARTMENT
  - SOC-Admin
  - SOC-Analyst

---

## 6.2 Groups

- SOC-Admins
- SOC-Analysts

---

## 6.3 Users

- socadmin
- socanalyst

Add to groups accordingly.

---

# 7. GPO Restrictions

## Allow log on locally:

- Administrators
- SOC-Admins
- SOC-Analysts

## Allow RDP:

- Administrators
- SOC-Admins
- SOC-Analysts

---

# 8. Dashboard Accounts

Create:

```text
socadmin@cyberrange.local
socanalyst@cyberrange.local
Password: Cyberrange2026
```

---

# 9. Time Sync Fix

If login fails:

- Align Security Onion time with Windows machines

---

# 10. Validation

## Security Onion

- IP reachable
- DNS correct

## Workstations

- Domain joined
- Can access dashboard

## Dashboard

- Loads correctly
- Login works

---

# Phase 01 Complete

Environment now includes:

- Security Onion monitoring platform
- SOC Admin workstation
- SOC Analyst workstation
- Domain-integrated SOC endpoints
- Functional dashboard access

---

# Next Phase

Remaining systems:

- Firewall & Segmentation Server
- Linux Log Server
- Adversary Simulation Server
- Core Router
- Traffic Generator
- Orchestration Server

---

End of Phase 01
