## Status

✅ Completed

# Marist SOC Cyber Range
# Lab Build Guide — Phase 01: Infrastructure, Virtualization, and Network Foundation

---

# Purpose

This document outlines the initial infrastructure setup for the Marist SOC Cyber Range.

This phase established the **core platform** that supports the entire environment, including:

- Virtualization (Proxmox)
- Network segmentation
- System architecture design
- Template preparation
- Initial connectivity validation

Everything built in later phases (Active Directory, file services, SOC tooling, attack simulation) depends on the decisions made here.

---

# 1. Environment Overview

## Hypervisor Platform

The cyber range is hosted on a Proxmox Virtual Environment (PVE) server.

### Node Information
- Node Name: `cyberrange`
- Access Method: Web UI (HTTPS)
- Managed via: Proxmox VE Dashboard

## Role of Proxmox

Proxmox serves as:

- Virtualization platform (hosts all VMs)
- Resource manager (CPU, RAM, Storage)
- Network bridge controller
- VM lifecycle manager

All systems in the cyber range are deployed, configured, and managed through Proxmox.

---

# 2. Network Architecture Design

## Objective

Design a segmented network that:

- Simulates a real enterprise environment
- Supports attack + defense workflows
- Maintains controlled isolation between environments

---

## Segmented Network Design

Three primary network zones were implemented:

### Red Team Network
- Subnet: `10.20.10.0/24`
- Bridge: `vmbr1`
- Purpose:
  - Attack simulation
  - Offensive tooling (Kali Linux)

---

### Target Network
- Subnet: `10.20.20.0/24`
- Bridge: `vmbr2`
- Purpose:
  - Enterprise simulation (AD, endpoints, servers)
  - Primary attack surface

---

### SOC / Detection Network
- Subnet: `10.20.30.0/24`
- Bridge: `vmbr3`
- Purpose:
  - Monitoring and detection
  - Security Onion and logging systems

---

## Why This Design Matters

This segmentation enables:

- Red Team → Target attack paths
- SOC → Target monitoring visibility
- Isolation between environments
- Realistic enterprise network simulation

This is one of the most critical design decisions in the entire project.

---

# 3. Firewall and Routing Layer

## Firewall Selection

A firewall/router system (OPNsense or pfSense) is used as the central network control point.

## Responsibilities

- Acts as default gateway for all subnets
- Routes traffic between environments
- Enforces segmentation policies
- Controls attack flow and visibility

---

## Why This Is Critical

This component enables:

- Realistic network boundaries
- Controlled attack scenarios
- Traffic inspection and analysis
- SOC visibility into Target activity

Without this layer, the environment would not behave like a real enterprise network.

---

# 4. Template Preparation

## Provided VM Templates

The following templates were available:

- `900 (kali-redteam)`
- `901 (Kali-Purple)`
- `902 (Ubuntu-Server24LTS)`
- `903 (Ubuntu-Desktop24LTS)`
- `904 (Windows-10-EduN)`
- `905 (Windows-11-EduN)`
- `906 (Windows-Server-2022)`

---

## Purpose of Templates

Templates allow:

- Rapid VM deployment
- Consistent configurations
- Scalable environment growth

---

## Best Practice

All systems in this environment are deployed by cloning templates.

This ensures:

- Standardization
- Reduced setup time
- Fewer configuration errors

---

# 5. Cyber Range Architecture Design

## Objective

Design a complete cyber range with three functional environments:

---

### Red Team Environment
Includes:

- Kali Linux machines
- Jump box

Purpose:

- Simulate attackers
- Execute exploits and reconnaissance

---

### Target Environment
Includes:

- Domain Controller
- File server
- Windows endpoints
- Vulnerable applications

Purpose:

- Simulate enterprise infrastructure
- Generate realistic activity
- Serve as attack target

---

### SOC / Detection Environment
Includes:

- Security Onion
- Logging tools
- Network monitoring systems

Purpose:

- Detect attacks
- Analyze behavior
- Provide visibility into the environment

---

## Architecture Outcome

This creates a full cyber range ecosystem:

- Attackers (Red Team)
- Victims (Target)
- Defenders (SOC)

---

# 6. Remote Access and Connectivity Validation

## Objective

Ensure all systems could be accessed and managed remotely.

---

## Actions Performed

- Verified VPN access into environment
- Tested RDP access to Windows systems
- Confirmed Proxmox web interface access
- Validated subnet communication

---

## Importance

This ensured:

- Remote management capability
- Team collaboration
- Reliable troubleshooting

---

# 7. Proxmox Familiarization

## Key Concepts Learned

- VM creation and cloning
- Template usage
- Resource allocation
- Network bridge assignment
- Console vs remote access

---

## Why This Matters

Proxmox is the control layer for:

- Infrastructure
- Networking
- System lifecycle

Misconfiguration here breaks everything downstream.

---

# 8. Key Design Decisions

## 1. Single Proxmox Server

Chosen because:

- Centralized management
- Reduced hardware complexity
- Easier deployment and maintenance

---

## 2. Network Segmentation

Chosen because:

- Enables isolation
- Supports realistic attack paths
- Improves scalability

---

## 3. Template-Based Deployment

Chosen because:

- Speeds up builds
- Ensures consistency
- Reduces manual errors

---

# 9. Key Lessons Learned

## 1. Planning is critical
Poor planning leads to major rework later.

## 2. Network design defines everything
A weak network architecture limits the entire project.

## 3. Templates are essential
They dramatically reduce build time.

## 4. Hypervisor knowledge is required
All systems depend on correct Proxmox configuration.

---

# 10. Final State After Phase 01

At the end of this phase:

- Proxmox environment was operational
- Network segmentation was implemented
- Firewall routing layer was introduced
- VM templates were ready
- Architecture was fully designed
- Remote access was validated

---

# 11. Current State (Post Phase 01)

The infrastructure defined in this phase is now actively supporting:

- Active Directory (Phase 02)
- Enterprise user/group structure (Phase 03)
- File server and access control (Phase 04)
- Ongoing SOC environment build

This confirms that the design decisions made in Phase 01 were correct and scalable.

---

# 12. Transition to Phase 02

Next phase:

- Deploy Windows Server
- Build Active Directory
- Create domain (`cyberrange.local`)
- Join endpoints

---

# 13. Quick Reference

## Networks

- Red Team → `10.20.10.0/24`
- Target → `10.20.20.0/24`
- SOC → `10.20.30.0/24`

## Bridges

- `vmbr1` → Red Team
- `vmbr2` → Target
- `vmbr3` → SOC

## Node

- `cyberrange`

---

# Conclusion

Phase 01 established the core infrastructure of the cyber range.

With virtualization, network segmentation, and architecture in place, the environment became capable of supporting:

- Enterprise identity systems
- User management
- Detection and monitoring
- Realistic cyber attack scenarios

This phase is the foundation of the entire project.
