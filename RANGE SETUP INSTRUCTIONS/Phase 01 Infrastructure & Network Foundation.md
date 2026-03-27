# Marist SOC Cyber Range
# Lab Build Guide — Infrastructure, Virtualization, and Network Foundation

## Purpose

This document outlines the initial infrastructure setup for the Marist SOC Cyber Range. It serves as the foundational phase of the project, where the virtualization environment, network segmentation, and base architecture were established.

This phase focused on:

- Preparing the Proxmox hypervisor environment
- Designing and implementing network segmentation
- Defining the cyber range architecture
- Establishing base VM templates
- Validating connectivity and remote access

This phase is critical because it provides the platform on which all future systems (Active Directory, SOC tooling, attack simulations) are built.

---

# 1. Environment Overview

## Hypervisor Platform

The cyber range is hosted on a Proxmox Virtual Environment (PVE) server.

### Node Information
- Node Name: `cyberrange`
- Access Method: Web UI (HTTPS)
- Managed via: Proxmox VE Dashboard

## Purpose of Proxmox

Proxmox acts as:
- The virtualization layer
- Resource manager (CPU, RAM, Storage)
- Network bridge controller
- VM lifecycle manager

All virtual machines in the cyber range are hosted within this environment.

---

# 2. Network Architecture Design

## Objective

The goal of the network design was to simulate a realistic enterprise environment while maintaining safe isolation between different functional zones.

## Segmented Network Design

Three primary network segments were defined:

### Red Team Network
- Subnet: `10.20.10.0/24`
- Purpose: Offensive operations (attack simulation)
- Proxmox Bridge: `vmbr1`

---

### Target Network
- Subnet: `10.20.20.0/24`
- Purpose: Simulated enterprise environment (users, servers)
- Proxmox Bridge: `vmbr2`

---

### SOC / Detection Network
- Subnet: `10.20.30.0/24`
- Purpose: Monitoring, logging, detection, and response
- Proxmox Bridge: `vmbr3`

---

## Why Network Segmentation Matters

This design allows:

- Controlled attack simulation from Red Team → Target
- Monitoring visibility from SOC → Target
- Isolation between environments to prevent unintended interference
- Realistic enterprise network modeling

---

# 3. Firewall and Routing Layer

## Firewall Selection

A firewall/router system (OPNsense or pfSense) is used to:

- Route traffic between subnets
- Enforce network segmentation rules
- Simulate enterprise perimeter security

## Responsibilities of the Firewall

- Default gateway for each subnet
- Traffic control between:
  - Red Team ↔ Target
  - Target ↔ SOC
- Policy enforcement for attack scenarios
- Network visibility and control

## Importance

This component acts as the **central control point** for all network communication and is essential for:

- Simulating real-world attack paths
- Implementing security controls
- Observing network traffic during scenarios

---

# 4. Template Preparation

## Provided VM Templates

The following templates were pre-configured and provided:

- `900 (kali-redteam)`
- `901 (Kali-Purple)`
- `902 (Ubuntu-Server24LTS)`
- `903 (Ubuntu-Desktop24LTS)`
- `904 (Windows-10-EduN)`
- `905 (Windows-11-EduN)`
- `906 (Windows-Server-2022)`

## Purpose of Templates

Templates allow:

- Rapid deployment of consistent virtual machines
- Standardized configurations across the environment
- Efficient scaling of the cyber range

## Best Practice

All VMs should be cloned from templates rather than built manually to ensure consistency and reduce configuration errors.

---

# 5. Cyber Range Architecture Design

## Objective

Design a realistic enterprise network that supports:

- Offensive (Red Team) activities
- Defensive (SOC) monitoring
- User and server simulation (Target environment)

## Environment Breakdown

### Red Team Environment
Includes:
- Kali Linux machines (students and instructor)
- Jump server for controlled access

Purpose:
- Launch attacks
- Perform reconnaissance
- Simulate adversary behavior

---

### Target Environment
Includes:
- Domain Controllers
- File servers
- Web servers
- User workstations (Windows 10/11)
- Vulnerable applications

Purpose:
- Simulate a real enterprise network
- Serve as the attack target
- Generate activity for detection

---

### SOC / Detection Environment
Includes:
- Security Onion
- Logging systems
- Intrusion detection tools
- Traffic analysis tools

Purpose:
- Monitor network activity
- Detect malicious behavior
- Analyze attack patterns

---

## Architecture Outcome

This design creates a full cyber range ecosystem:

- Attackers (Red Team)
- Victims (Target)
- Defenders (SOC)

---

# 6. Remote Access and Connectivity Validation

## Objective

Ensure that systems within the environment could be accessed and managed remotely.

## Actions Performed

- Verified VPN access into the environment
- Tested RDP connectivity to Windows systems
- Confirmed access to Proxmox web interface
- Validated basic network communication between systems

## Importance

Without reliable remote access:

- Systems cannot be managed efficiently
- Troubleshooting becomes difficult
- Collaboration across the team is limited

---

# 7. Initial Proxmox Familiarization

## Key Concepts Learned

- VM creation and cloning
- Template usage
- Hardware configuration (CPU, RAM, Disk)
- Network interface assignment (vmbr bridges)
- Console access vs remote access

## Why This Matters

Understanding Proxmox is essential because:

- All infrastructure changes occur here
- Network placement is controlled here
- VM lifecycle (start, stop, clone, delete) is managed here

---

# 8. Key Design Decisions

## 1. Use of a Single Proxmox Server

Chosen because:
- Simplifies management
- Centralizes resources
- Reduces hardware requirements

## 2. Network Segmentation via Bridges

Chosen because:
- Enables isolation
- Supports realistic attack paths
- Provides flexibility for future expansion

## 3. Template-Based Deployment

Chosen because:
- Reduces setup time
- Ensures consistency
- Simplifies scaling

---

# 9. Key Lessons Learned

## 1. Planning is critical
Designing the architecture before building prevents rework and confusion later.

## 2. Network segmentation is foundational
A poorly designed network makes it difficult to simulate attacks and monitor behavior effectively.

## 3. Templates save significant time
Using prebuilt images avoids repetitive OS installation and configuration.

## 4. Understanding the hypervisor is essential
All infrastructure depends on correct Proxmox configuration.

---

# 10. Final State After Phase 01

By the end of this phase:

- Proxmox environment was fully accessible
- Network segmentation was defined and implemented
- Firewall/routing layer was introduced
- VM templates were available for cloning
- Cyber range architecture was designed
- Remote access and connectivity were validated

---

# 11. Transition to Phase 02

With infrastructure in place, the next phase focused on:

- Deploying Windows Server
- Building Active Directory
- Creating a domain environment
- Joining workstations to the domain

---

# 12. Quick Reference

## Networks

- Red Team: `10.20.10.0/24`
- Target: `10.20.20.0/24`
- SOC: `10.20.30.0/24`

## Proxmox Bridges

- `vmbr1` → Red Team
- `vmbr2` → Target
- `vmbr3` → SOC

## Node

- `cyberrange`

---

# Conclusion

Phase 01 established the foundational infrastructure required to build a fully functional cyber range. With virtualization, network segmentation, and architecture in place, the environment was ready to support enterprise services such as Active Directory, user management, and security monitoring in subsequent phases.
