# Target Environment Setup

This environment simulates a fully built enterprise network designed for cybersecurity training, attack simulation, and SOC monitoring.

---

## Status

✅ COMPLETE

The Target Environment has been fully built, validated, and is ready for SOC / Detection integration.

---

## Build Progress

- ✅ IP Configuration Defined
- ✅ Network Segmentation Implemented
- ✅ Domain Controller Deployment
- ✅ Active Directory & DNS Configuration
- ✅ Windows 10 Deployment (3 Systems)
- ✅ Windows 11 Deployment (3 Systems)
- ✅ Active Directory Structure (OUs, Users, Groups)
- ✅ Group Policy Deployment & Validation
- ✅ Audit Logging Enabled & Verified
- ✅ File Server Deployment
- ✅ Enterprise Share Structure Created
- ✅ Group-Based Access Control Implemented
- ✅ Backup Domain Controller Deployment
- ✅ Internal Web Server Deployment
- ✅ Windows Log Server Deployment (Prepared)
- ✅ IT Admin Workstation Deployment
- ✅ Incident Response Workstation Deployment
- ✅ Vulnerable Training Server Deployment (Docker-based application)
- ✅ Blue Team Analysis Workstation (Kali Purple)
- ✅ Full Target Environment Validation Completed

---

## Build Order

1. `ip_configuration.md`  
2. `phase_01_networking.md`  
3. `phase_02_active_directory.md`  
4. `phase_03_ad_structure_gpo.md`  
5. `phase_04_file_server.md`  
6. `phase_05_target_completion.md`  

---

## Systems Included

### Core Infrastructure
- Primary-Domain-Server (DNS)
- Backup-Domain-Server (DNS)
- File-Server
- Internal Web Server
- Windows Log Server

### Endpoints
- Windows 10 Workstations (3)
- Windows 11 Workstations (3)

### Administrative & Defensive Systems
- IT Admin Workstation
- Incident Response Workstation
- Blue Team Analysis Workstation (Kali Purple)

### Attack Surface
- Vulnerable Training Server (DVWA / Juice Shop via Docker)

---

## Network Design Notes

- DHCP is managed externally (not on domain controllers)
- All domain-joined systems use:
  - Primary DNS: `10.20.20.10`
  - Secondary DNS: `10.20.20.11`
- Servers use static IP addressing
- Client systems use DHCP for dynamic assignment

---

## Current Completion State

The Target Environment is now fully operational and represents a realistic enterprise network.

All systems are:

- Built and configured  
- Network connected  
- Domain integrated (where applicable)  
- Functionally validated  

---

### Completed

- Full Active Directory environment
- Domain-joined endpoints
- Group Policy enforcement
- Audit logging and verification
- Enterprise file services and permissions
- Redundant domain infrastructure
- Internal web services
- Centralized log server preparation
- Administrative and IR workstations
- Blue team analysis workstation
- Vulnerable application environment (Docker-based deployment)
- Full inter-system connectivity validation

---

### In Progress

None

---

## Next Phase

SOC / Detection Environment Setup

This phase will introduce:

- Security Onion deployment
- Log ingestion and aggregation
- Network and host monitoring
- Detection engineering
- Scenario-based attack and response workflows

---

## Goal

To replicate a realistic enterprise network that supports:

- Cybersecurity training  
- Attack simulation (Red Team)  
- Detection and monitoring (SOC)  
- Incident response workflows  

This environment serves as the foundation for all future security operations and analysis within the cyber range.
