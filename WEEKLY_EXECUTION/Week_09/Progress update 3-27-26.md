# Marist SOC Cyber Range — Progress Update

## Overview

Today focused on building the foundational infrastructure of the cyber range inside Proxmox. The primary goal was to establish a working Active Directory environment and successfully integrate Windows endpoints into a centralized domain.

---

## 1. VM Deployment & Initial Setup

* Rebuilt the environment from scratch using provided Proxmox templates to ensure consistency and eliminate earlier configuration confusion.
* Successfully cloned and deployed the following core systems:

  * Primary Domain Controller (Windows Server 2022)
  * Windows 10 User Machine
  * Windows 11 User Machine
* Verified correct network segmentation based on predefined architecture:

  * `vmbr1` → Red Team
  * `vmbr2` → Target Environment
  * `vmbr3` → SOC/Detection

---

## 2. Windows Server (Domain Controller) Configuration

* Installed Windows Server 2022 successfully using VirtIO drivers.
* Configured:

  * Static IP: `10.20.20.10`
  * Subnet: `255.255.255.0`
  * Gateway: `10.20.20.1`
* Installed required roles:

  * Active Directory Domain Services (AD DS)
  * DNS Server
* Promoted server to Domain Controller:

  * Created new forest: `cyberrange.local`
* Verified successful deployment:

  * DNS zones automatically created
  * Domain Controller operational
  * Authentication confirmed via `whoami`

---

## 3. Network & Driver Configuration

* Installed all required VirtIO drivers:

  * Network adapter (critical for connectivity)
  * PCI / system drivers
* Verified:

  * Network adapter properly recognized
  * IP configuration functioning
* Resolved initial connectivity issues:

  * Confirmed communication between endpoints and Domain Controller using `ping`
  * Verified ARP and gateway presence

---

## 4. Domain Join (Windows 10 & Windows 11)

* Configured both endpoints with:

  * Static IP addresses within `10.20.20.0/24`
  * DNS pointing to Domain Controller (`10.20.20.10`)
* Successfully joined both machines to:

  * `cyberrange.local`
* Verified:

  * Machines appear in Active Directory
  * Domain authentication works
  * Login using domain account (`cyberrange\itadmin`) successful

---

## 5. Active Directory Validation

* Confirmed:

  * Domain structure operational
  * Devices visible in AD Users and Computers
  * DNS resolution functioning across machines
* Organized machines into appropriate OUs (in progress)

---

## Key Achievements

* Fully operational Active Directory environment
* Functional DNS and domain-based authentication
* Multiple endpoints successfully joined to domain
* Verified internal network communication
* Established foundation for enterprise simulation

---

## Next Steps

* Create Organizational Units (OUs)
* Add users and security groups
* Implement Group Policy (GPOs)
* Expand environment (servers, logging, SOC tools)
* Begin attack/defense simulation setup

---

## Notes

* Standardized password used for lab simplicity: `Cyberrange2026`
* Environment is now stable and ready for expansion into full cyber range operations

---

## Summary

Today transitioned the project from infrastructure setup to a functioning enterprise network. The environment now supports centralized identity management and provides the foundation required for both offensive (Red Team) and defensive (SOC) operations.

---
